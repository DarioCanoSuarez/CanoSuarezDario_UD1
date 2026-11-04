# E03 · Compilado, interpretado y máquina virtual

## Qué genera cada lenguaje

| Lenguaje | Comando de compilación / traducción | Fichero nuevo generado | Qué hace falta para ejecutarlo | Salida del programa |
| :--- | :--- | :--- | :--- | :--- |
| **Java** | `javac Primos.java` | `Primos.class` (Bytecode) | Entorno de ejecución de Java (JVM / `java`) | `Primos menores que 10000: 1229` |
| **Python** | `python -m py_compile primos.py` | Carpeta `__pycache__/` con `primos.cpython-3XX.pyc` | Interprete de Python (`python` / `python3`) | `Primos menores que 10000: 1229` |
| **C** | `gcc primos.c -o primos` | `primos` (o `primos.exe` en Windows) | Nada más (se ejecuta directamente en el S.O.) | `Primos menores que 10000: 1229` |

## Clasificación

| Lenguaje | Paradigma principal | Tipado | Forma de ejecución |
| :--- | :--- | :--- | :--- |
| **Java** | Orientado a objetos | Estático | Máquina virtual |
| **Python** | Multiparadigma (Orientado a objetos / Imperativo) | Dinámico | Interpretado (compila previamente a bytecode en memoria) |
| **C** | Imperativo / Procedural | Estático | Compilado |

## Los diez primeros del índice TIOBE

* **Fecha de consulta:** 4 de noviembre de 2026  
* **Mes del índice:** Noviembre 2026  

| Posición | Lenguaje | Paradigma principal | Tipado | Forma de ejecución | Uso habitual |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | Python | Multiparadigma | Dinámico | Interpretado (con bytecode interno) | Inteligencia Artificial, Data Science y desarrollo web |
| **2** | C | Imperativo / Procedural | Estático | Compilado | Sistemas operativos, controladores y sistemas embebidos |
| **3** | C++ | Multiparadigma (POO / Genérico) | Estático | Compilado | Videojuegos, motores gráficos y software de alto rendimiento |
| **4** | Java | Orientado a objetos | Estático | Máquina virtual | Aplicaciones empresariales y desarrollo Android |
| **5** | C# | Multiparadigma (POO / Funcional) | Estático | Máquina virtual (.NET CLR) | Desarrollo en el entorno Microsoft, videojuegos (Unity) |
| **6** | JavaScript | Multiparadigma (Basado en prototipos) | Dinámico | Interpretado / JIT (Máquina Virtual en navegador) | Desarrollo web frontend y backend (Node.js) |
| **7** | Visual Basic | Orientado a objetos / Eventos | Estático | Máquina virtual (.NET CLR) | Aplicaciones de escritorio administrativas y macros de Office |
| **8** | SQL | Declarativo / Consulta | Estático | Interpretado (por el motor de la base de datos) | Gestión y consulta de bases de datos relacionales |
| **9** | R | Multiparadigma (Funcional / Vectorial) | Dinámico | Interpretado | Análisis estadístico, minería de datos e investigación |
| **10** | Rust | Multiparadigma (Funcional / Sistemas) | Estático | Compilado | Programación de sistemas seguros, infraestructura web y concurrencia |

## Preguntas

1. **¿Qué diferencias principales existen entre un lenguaje compilado, uno interpretado y uno basado en máquina virtual?**
   - **Compilado:** Un compilador traduce el código fuente directamente a lenguaje máquina específico para la arquitectura del sistema operativo y procesador. Se ejecuta de forma nativa sin intermediarios y con máximo rendimiento.
   - **Interpretado:** Un intérprete lee el código fuente instrucción por instrucción durante el tiempo de ejecución y lo traduce al vuelo. Ofrece gran portabilidad pero suele tener menor rendimiento.
   - **Máquina virtual:** El código se compila previamente a un código intermedio independiente del hardware (llamado *bytecode*). Una máquina virtual (como la JVM) se encarga de interpretar o compilar en tiempo de ejecución (JIT) dicho bytecode para la plataforma en la que se ejecuta.

2. **A la vista del paso de Python (`python -m py_compile primos.py`), ¿es estrictamente cierto que Python nunca compila el código? Explícalo.**
   No, no es estrictamente cierto. Aunque Python es considerado un lenguaje interpretado, internamente siempre compila el código fuente a una representación intermedia llamada *bytecode* (ficheros `.pyc`). Por defecto guarda este bytecode en memoria (o en la carpeta `__pycache__` al importar módulos) para no tener que parsear la sintaxis cada vez que se ejecuta el código.
