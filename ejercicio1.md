# E01 · Un programa por dentro

## Salida del programa

```texto
¿Cuántas notas? 4
Nota 1: 6
Nota 2: 8
Nota 3: 9
Nota 4: 5
Media: 7.0
```

## El proceso

Proceso de Java localizado mientras el programa esperaba en `¿Cuántas notas?`:

| Dato | Valor |
|------|-------|
| Nombre del proceso | `java` |
| PID | 352 |
| Uso de CPU | 0 % (0 ticks de CPU en 3 s de espera) |
| Memoria | 89 256 kB (≈ 87 MB) |
| Estado | `S` (sleeping): bloqueado esperando el teclado |
| Hilos | 19 |

Captura: `img/proceso.png`

![Proceso de Java](img/proceso.png)

**Explicación:** mientras espera el teclado, el proceso está **bloqueado**: el sistema operativo lo saca de la CPU hasta que llegue una pulsación, por eso consume casi 0 % de procesador. Aun así sigue ocupando memoria, sobre todo la de la propia JVM (código de la máquina virtual, clases cargadas, montículo reservado, pilas de hilos).

## Componentes en cada paso

| # | Paso del programa | Qué ocurre | Componentes que intervienen | Zona de memoria |
|---|-------------------|------------|-----------------------------|-----------------|
| 1 | `java Media.java` | El SO crea el proceso, arranca la JVM, que compila el fichero en memoria y lo ejecuta | Sistema operativo, disco (lee `Media.java`), CPU, RAM | Código y clases cargadas en memoria de la JVM; sin `.class` en disco |
| 2 | Crear el `Scanner` (`new Scanner(System.in)`) | Se crea el objeto que lee de la entrada estándar | CPU, RAM | Objeto en el **montículo**; la referencia (variable `teclado`) en la **pila** |
| 3 | Mostrar `¿Cuántas notas?` | El programa pide al SO escribir en la pantalla | CPU, sistema operativo (llamada al sistema), controlador de la terminal, pantalla | Cadena en el montículo; nada nuevo en la pila |
| 4 | Leer `cantidad` | El programa espera; el proceso se bloquea hasta pulsar Enter; se guarda el número | Teclado, controlador, sistema operativo (llamada al sistema, planificador), CPU | Variable `cantidad` en la **pila** (trama de `main`) |
| 5 | Crear el array `notas` (`new int[cantidad]`) | Se reserva memoria para `cantidad` enteros | CPU, JVM, RAM | Array en el **montículo**; variable `notas` (referencia) en la **pila** |
| 6 | Pedir cada nota (bucle) | Por cada vuelta: se muestra el texto, se lee la nota y se guarda en el array | Teclado, pantalla, sistema operativo, CPU | Valores en el array (**montículo**); variables `nota` e `i` en la **pila** |
| 7 | Llamar a `calcularMedia(notas)` | La JVM crea una trama nueva en la pila y pasa la referencia al array | CPU, JVM | Nueva **trama** en la **pila**; el array sigue en el **montículo** |
| 8 | Calcular `suma` y la media dentro de `calcularMedia` | Se recorre el array sumando y se divide entre la cantidad; al devolver, la trama desaparece | CPU (ALU, registros), RAM | Variable `suma` en la **pila** (trama de `calcularMedia`); el resultado vuelve a `main` |
| 9 | Mostrar `Media: 7.0` | Se guarda `media` y se imprime el resultado por la terminal; el programa termina | CPU, sistema operativo (llamada al sistema), controlador, pantalla | `media` en la **pila**; texto en el montículo; al terminar, el SO libera la memoria del proceso |

## Cuando se acaba la memoria

Orden: `java -Xmx64m Media.java`, y `100000000` como cantidad.

```text
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
at Media.main(Media.java:8)
```

**Qué ha pasado:** el error es `java.lang.OutOfMemoryError: Java heap space`, y se produce en la línea 8, la que crea el array (`new int[cantidad]`). Un `int` ocupa 4 bytes, así que cien millones de enteros necesitan unos 400 MB, y con `-Xmx64m` el montículo no puede pasar de 64 MB. La JVM no encuentra un bloque libre tan grande, no puede reservarlo y lanza el error; el programa termina sin llegar a pedir ninguna nota.

## Preguntas

1. **¿Dónde está la variable `notas` y dónde el array al que apunta?** La variable (la referencia) está en la pila, en la trama de `main`; el array está en el montículo.
2. **¿Qué pasa en la pila al llamar a `calcularMedia`?** Se crea una trama nueva con sus variables locales (`suma`...). Al devolver la media, esa trama desaparece.
3. **¿Por qué el proceso usa casi 0 % de CPU mientras espera?** Porque está bloqueado esperando el teclado: el sistema operativo no le da CPU hasta que haya datos de entrada.
4. **¿Qué pasos pasan por el sistema operativo?** Los que muestran texto y los que leen del teclado, mediante llamadas al sistema y controladores.
