# E02 · Compilar, ejecutar y empaquetar a mano

## Versiones
```bash
$ java -version
java version "17.0.9" 2023-10-17 LTS
Java(TM) SE Runtime Environment (build 17.0.9+11-LTS-201)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.9+11-LTS-201, mixed mode, sharing)

$ javac -version
javac 17.0.9
```

## Compilar
Comando ejecutado:
```bash
javac -d out src/endes/calificaciones/Calificacion.java src/endes/calificaciones/Main.java
```

Ficheros creados y su ubicación:
- `out/endes/calificaciones/Calificacion.class`
- `out/endes/calificaciones/Main.class`

## Ejecución
Comando ejecutado:
```bash
java -cp out endes.calificaciones.Main
```

Salida obtenida:
```text
Tabla de calificaciones:
3.5 -> Insuficiente
5.0 -> Suficiente
6.5 -> Bien
7.5 -> Notable
9.0 -> Sobresaliente
11.0 -> Nota no válida
```

## El bytecode
Comando ejecutado:
```bash
javap -c -cp out endes.calificaciones.Calificacion
```

Instrucciones del método `calificar` (líneas 0 a 16):
```text
 0: dload_0
 1: dconst_0
 2: dcmpg
 3: iflt          16
 6: dload_0
 7: ldc2_w        #7                  // double 10.0d
10: dcmpg
11: ifle          20
16: ldc           #9                  // String Nota no válida
```

**Explicación:**
- `0: dload_0`: Carga en la pila local la variable de tipo `double` recibida en el parámetro 0 (la nota).
- `1: dconst_0`: Carga la constante numérica decimal `0.0` en la pila.
- `2: dcmpg`: Compara los dos números `double` cargados en la pila.
- `3: iflt 16`: Si la nota es menor que 0 (`iflt` - if less than), salta a la instrucción de la línea 16.
- `6: dload_0`: Vuelve a cargar el valor de la nota en la pila.
- `7: ldc2_w #7`: Carga la constante `10.0d` desde la tabla de constantes.
- `10: dcmpg`: Compara la nota con `10.0`.
- `11: ifle 20`: Si es menor o igual a `10.0` (`ifle`), salta a la evaluación del siguiente rango (línea 20).
- `16: ldc #9`: Carga la cadena constante `"Nota no válida"` para devolverla.

## Empaquetado JAR
Comandos ejecutados y sus salidas:

1. Crear JAR:
```bash
jar --create --file calificaciones.jar --main-class endes.calificaciones.Main -C out .
```

2. Listar contenido del JAR:
```bash
jar --list --file calificaciones.jar
```
Salida:
```text
META-INF/
META-INF/MANIFEST.MF
endes/
endes/calificaciones/
endes/calificaciones/Calificacion.class
endes/calificaciones/Main.class
```

3. Ejecutar archivo JAR:
```bash
java -jar calificaciones.jar
```
Salida:
```text
Tabla de calificaciones:
3.5 -> Insuficiente
5.0 -> Suficiente
6.5 -> Bien
7.5 -> Notable
9.0 -> Sobresaliente
11.0 -> Nota no válida
```

## Errores provocados

| Prueba | Comando ejecutado | Primera línea del mensaje de error | Tipo de error | Herramienta que lo detecta |
| :--- | :--- | :--- | :--- | :--- |
| **1. Quitar `;` en `return "Bien"`** | `javac -d out src/endes/calificaciones/Calificacion.java src/endes/calificaciones/Main.java` | `src/endes/calificaciones/Calificacion.java:15: error: ';' expected` | Compilación (Sintáctico) | `javac` |
| **2. Cambiar nombre del método** | `javac -d out src/endes/calificaciones/Calificacion.java src/endes/calificaciones/Main.java` | `src/endes/calificaciones/Main.java:10: error: cannot find symbol` | Compilación (Semántico) | `javac` |
| **3. Borrar `.class` y ejecutar** | `rm out/endes/calificaciones/Calificacion.class`<br>`java -cp out endes.calificaciones.Main` | `Exception in thread "main" java.lang.NoClassDefFoundError: endes/calificaciones/Calificacion` | Ejecución | JVM (`java`) |
| **4. Ejecutar sin paquete** | `java -cp out Main` | `Error: Could not find or load main class Main` | Ejecución | JVM (`java`) |

## Preguntas

**1. ¿Por qué el código fuente Java se compila a bytecode (`.class`) en lugar de a código máquina binario específico del procesador?**
Porque el bytecode es un formato intermedio independiente de la plataforma y del hardware. Esto permite cumplir el principio de Java "Escribe una vez, ejecútalo en cualquier lugar" (*Write Once, Run Anywhere*). Cualquier sistema informático que disponga de una Máquina Virtual de Java (JVM) puede interpretar o compilar a código máquina nativo dicho bytecode sin necesidad de volver a compilar el código fuente original.

**2. ¿Qué función cumple la Máquina Virtual de Java (JVM) al ejecutar un programa?**
La JVM es la encargada de cargar los archivos de bytecode (`.class`), verificar su seguridad, gestionar la memoria y traducir cada instrucción del bytecode a código máquina que el procesador físico de la máquina host pueda ejecutar en tiempo real (mediante interpretación o compilación JIT).

**3. En el error 3, ¿por qué la línea "Tabla de calificaciones:" sí llega a imprimirse por pantalla antes de que el programa falle?**
Porque la JVM utiliza una carga perezosa (*lazy loading*) de clases. La clase `Main` se ejecuta e imprime por consola la primera línea `"Tabla de calificaciones:"` antes de intentar hacer uso de la clase `Calificacion`. Cuando el flujo del programa llega a la línea que requiere invocar un método estático de `Calificacion`, es cuando la JVM intenta cargar `Calificacion.class` en memoria, no la encuentra y lanza el error `NoClassDefFoundError`.
