# E07 · Radiografía de un proyecto de software libre (integrador)

## Proyecto analizado

* **Nombre del proyecto**: jsoup
* **Repositorio**: [https://github.com/jhy/jsoup](https://github.com/jhy/jsoup)
* **Licencia**: Licencia MIT ([Evidencia: LICENSE](https://github.com/jhy/jsoup/blob/master/LICENSE))
* **Última versión publicada**: `jsoup-1.18.3` (Publicada el 27 de octubre de 2024) ([Evidencia: Release 1.18.3](https://github.com/jhy/jsoup/releases/tag/jsoup-1.18.3))
* **Fecha de consulta**: 04 de noviembre de 2026

---

## 1. El programa y el sistema

* **Tipo de software**: Software de desarrollo (Biblioteca / Librería de software). Es un analizador (parser) de HTML en Java que proporciona una API para extraer y manipular datos estructurados.
* **Carácter multiplataforma**: Es totalmente multiplataforma porque está escrita integramente en Java puro y empaquetada como un archivo JAR independiente. Se ejecuta sobre cualquier sistema operativo que disponga de una Máquina Virtual de Java (JVM).
* **Recursos del sistema que utiliza**:
  1. **Red (Sockets / HTTP)**: Realiza peticiones HTTP/HTTPS para descargar páginas web remotas.  
     *[Evidencia en código: HttpConnection.java](https://github.com/jhy/jsoup/blob/master/src/main/java/org/jsoup/helper/HttpConnection.java)*
  2. **Sistema de Ficheros (I/O)**: Lee y parsea archivos `.html` almacenados en el disco local mediante flujos de entrada.  
     *[Evidencia en código: Jsoup.java - método parse(File)](https://github.com/jhy/jsoup/blob/master/src/main/java/org/jsoup/Jsoup.java#L101)*

---

## 2. Lenguajes

### Lenguajes detectados por GitHub
*(Datos obtenidos del apartado Languages en el repositorio)*

| Lenguaje | Porcentaje | Uso en el proyecto |
|---|---|---|
| **Java** | ~99.1% | Código fuente de la biblioteca, pruebas unitarias y componentes auxiliares. |
| **HTML** | ~0.6% | Ficheros HTML de ejemplo utilizados como casos de prueba en el conjunto de tests. |
| **Shell** | ~0.3% | Scripts de automatización de entorno y ejecutable Maven Wrapper (`mvnw`). |

### Clasificación del lenguaje principal (Java)
* **Nivel**: Alto nivel (abstrae la gestión directa de memoria del procesador).
* **Generación**: 3ª Generación (3GL).
* **Paradigma**: Orientado a Objetos (POO), multiparadigma (soporta características funcionales desde Java 8).
* **Tipado**: Estático y fuerte.
* **Forma de ejecución**: Mixta mediante Máquina Virtual (Compilado a Bytecode `.class` que la JVM interpreta y/o compila JIT a código máquina).

---

## 3. Del código al ejecutable

* **Herramienta de construcción**: Apache Maven.
* **Fichero de configuración**: `pom.xml` ([Evidencia: pom.xml](https://github.com/jhy/jsoup/blob/master/pom.xml)).
* **Versión mínima de Java exigida**: Java 8 (`<maven.compiler.target>1.8</maven.compiler.target>`) ([Evidencia: Configuración de compilador en pom.xml](https://github.com/jhy/jsoup/blob/master/pom.xml#L33)).
* **Artefacto distribuido y destino**: Se distribuye como un paquete JAR ejecutable/importable (`jsoup-1.18.3.jar`) publicado en el repositorio central de Maven (Maven Central) y en GitHub Releases ([Evidencia: Deploy a Maven Central en GitHub Actions](https://github.com/jhy/jsoup/blob/master/.github/workflows/deploy.yml)).

### Camino completo desde el código fuente hasta la ejecución
1. **Edición**: El desarrollador escribe el código Java (`.java`) en el directorio `src/main/java/`.
2. **Compilación**: Maven invoca `javac`, transformando el código fuente en instrucciones bytecode intermedias almacenadas en ficheros `.class`.
3. **Empaquetado**: Maven empaqueta las clases compiladas junto con sus metadatos (`MANIFEST.MF`) en un único archivo comprimido `.jar`.
4. **Distribución**: El `.jar` se publica en Maven Central.
5. **Ejecución y Portabilidad**: El usuario descarga el archivo `.jar` y lo añade al *classpath* de su aplicación. Cuando la aplicación corre, la JVM del sistema operativo destino (Windows, GNU/Linux o macOS) lee el bytecode ejecutable universal y el compilador Just-In-Time (JIT) de la JVM lo traduce a código máquina nativo específico de la arquitectura del procesador huésped.

---

## 4. Fases del desarrollo

| Fase | Evidencia en el proyecto (Enlace concreto) | Qué muestra la evidencia |
|---|---|---|
| **Análisis de requisitos** | [Issue #2135: Add support for custom HTTP headers](https://github.com/jhy/jsoup/issues/2135) | Una solicitud/discusión de funcionalidad por parte de los usuarios expresando sus necesidades. |
| **Diseño y modelado** | [Javadoc Oficial de Jsoup](https://jsoup.org/apidocs/org/jsoup/select/Elements.html) | La definición estructurada de las clases, jerarquías de paquetes y arquitectura de la API. |
| **Codificación / Desarrollo** | [Commit en Parser.java](https://github.com/jhy/jsoup/commit/e7f4c9c148815144fbb7df61a93bd8ce2948ff06) | Cambios directos en el código fuente Java implementando lógica y correcciones. |
| **Pruebas (Testing)** | [Directory src/test/java](https://github.com/jhy/jsoup/tree/master/src/test/java/org/jsoup) | Conjunto de pruebas unitarias automatizadas escritas con JUnit para validar componentes. |
| **Construcción / Despliegue** | [Workflow build.yml](https://github.com/jhy/jsoup/blob/master/.github/workflows/build.yml) | Automatización del proceso de compilación, ejecución de tests y empaquetado en CI. |
| **Explotación / Operación** | [Guía de inicio en jsoup.org](https://jsoup.org/cookbook/extracting-data/attributes) | Documentación y guías dirigidas a los usuarios finales para integrar y utilizar la biblioteca. |
| **Mantenimiento** | [PR #2130: Fix memory leak in TokenQueue](https://github.com/jhy/jsoup/pull/2130) | Modificación del código para resolver un fallo reportado por los usuarios. |

### Cambio de mantenimiento clasificado
* **Cambio analizado**: [Pull Request #2130](https://github.com/jhy/jsoup/pull/2130)
* **Tipo de mantenimiento**: **Correctivo**.
* **Justificación**: Modifica la lógica de consumo de tokens para solucionar una fuga de memoria detectada durante el uso continuado, corrigiendo un defecto del sistema sin añadir nuevas funcionalidades.

---

## 5. Metodología

### Prácticas ágiles identificadas

| Práctica ágil | Evidencia (Enlace concreto) | Observaciones |
|---|---|---|
| **Entregas frecuentes** | [Historial de Releases de jsoup](https://github.com/jhy/jsoup/releases) | Publicación constante de versiones incrementales con mejoras acumuladas. |
| **Revisión de cambios** | [Pull Request #2140](https://github.com/jhy/jsoup/pull/2140) | Revisiones de código (*Code Review*) con comentarios antes de integrar los cambios en la rama principal. |
| **Integración Continua (CI)** | [GitHub Actions Runs](https://github.com/jhy/jsoup/actions) | Ejecución automática de baterías de tests ante cada *push* o *pull request*. |
| **Participación de usuarios** | [GitHub Discussions en jsoup](https://github.com/jhy/jsoup/discussions) | Canal directo de diálogo entre la comunidad de usuarios y el mantenedor principal. |
| **Planificación visible** | [Milestones de jsoup](https://github.com/jhy/jsoup/milestones) | Agrupación de incidencias y tareas asociadas a las próximas versiones de la biblioteca. |

### Conclusión sobre la metodología
El proyecto jsoup no aplica una metodología estricta con eventos presenciales como Scrum (ya que carece de sprints cerrados de tiempo o ceremonias rígidas), sino que sigue una metodología ágil orientada a **Kanban / Desarrollo Guiado por Funcionalidad (FDD)** en software libre. Este enfoque se adapta perfectamente al desarrollo *open source*, permitiendo integrar contribuciones asíncronas de la comunidad, mantener integración continua de calidad y lanzar iteraciones de manera flexible.

---

## 6. Herramientas

### Inventario de herramientas por fase

| Herramienta | Fase de desarrollo | Para qué se usa | Fichero / Enlace de evidencia |
|---|---|---|---|
| **GitHub Issues** | Análisis de requisitos | Gestión de peticiones de características y reporte de fallos. | [Incidencias del proyecto](https://github.com/jhy/jsoup/issues) |
| **Git** | Control de versiones | Seguimiento del historial de cambios del código fuente. | [Historial de Commits](https://github.com/jhy/jsoup/commits/master) |
| **Apache Maven** | Construcción | Gestión de dependencias, compilación y empaquetado. | [pom.xml](https://github.com/jhy/jsoup/blob/master/pom.xml) |
| **JUnit 5** | Pruebas (Testing) | Marco para la definición y ejecución de pruebas unitarias. | [Pom.xml - Dependencia JUnit](https://github.com/jhy/jsoup/blob/master/pom.xml#L80) |
| **GitHub Actions** | Integración / Despliegue | Integración continua, ejecución de tests y despliegue automático. | [.github/workflows/build.yml](https://github.com/jhy/jsoup/blob/master/.github/workflows/build.yml) |
| **Javadoc** | Documentación | Generación automática de la documentación de la API en HTML. | [Javadoc target en pom.xml](https://github.com/jhy/jsoup/blob/master/pom.xml#L145) |

### Evaluación de una herramienta: GitHub Actions

* **Herramienta evaluada**: GitHub Actions
* **Fecha de consulta de datos**: 04 de noviembre de 2026
* **Criterios de evaluación**:
  1. **Integración con el repositorio (Peso: 3)**: Al estar integrado nativamente en GitHub, elimina la necesidad de configurar servidores de CI externos como Jenkins, automatizando disparadores en cada PR ([Fuente: Workflow build.yml](https://github.com/jhy/jsoup/blob/master/.github/workflows/build.yml)). Puntuación: 5/5.
  2. **Multiplataforma y matrices de compilación (Peso: 3)**: Permite probar el código simultáneamente en entornos Linux, macOS y Windows con diferentes JDKs (Java 8, 11, 17, 21) ([Fuente: Matriz de ejecución en build.yml](https://github.com/jhy/jsoup/blob/master/.github/workflows/build.yml#L18)). Puntuación: 5/5.
  3. **Coste y cuotas para Código Abierto (Peso: 2)**: Es completamente gratuito e ilimitado para repositorios públicos de código abierto ([Fuente: GitHub Pricing Docs](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions)). Puntuación: 5/5.

---

## Conclusión

El análisis del proyecto jsoup demuestra que el desarrollo de software profesional va mucho más allá de escribir código Java: requiere una infraestructura automatizada de construcción y pruebas (Maven y JUnit), una gestión rigurosa del control de versiones y una tubería de integración continua (GitHub Actions) que garantice la calidad de cada cambio antes de empaquetar y distribuir el bytecode ejecutable a miles de usuarios.
