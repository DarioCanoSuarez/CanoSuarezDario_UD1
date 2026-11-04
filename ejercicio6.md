# E06 · La caja de herramientas

## Herramientas por fase

| Fase del desarrollo | Herramienta | Qué hace | Licencia | Plataformas |
|---|---|---|---|---|
| **Análisis de requisitos** | Jira | Gestión de requisitos, captura de historias de usuario y trazabilidad del proyecto. | Propietaria (SaaS / Freemium) | Web, iOS, Android |
| **Diseño y modelado** | StarUML | Creación y edición de diagramas de modelos UML y SysML. | Propietaria (Evaluación gratuita / Pago) | Windows, macOS, Linux |
| **Codificación / Desarrollo** | Visual Studio Code | Editor de código fuente extensible con soporte para múltiples lenguajes y depuración. | MIT (Código fuente) / Propietaria (Binario distribuido) | Windows, macOS, Linux |
| **Control de versiones** | Git | Sistema de control de versiones distribuido para rastrear cambios en el código. | GPLv2 | Windows, macOS, Linux |
| **Construcción / Automatización** | Apache Maven | Gestión de dependencias y automatización del ciclo de vida de construcción en Java. | Apache License 2.0 | Multiplataforma (JVM) |
| **Pruebas (Testing)** | JUnit 5 | Framework de pruebas unitarias para proyectos y aplicaciones en lenguaje Java. | Eclipse Public License v2.0 | Multiplataforma (JVM) |
| **Despliegue / Integración continua** | GitHub Actions | Automatización de flujos de trabajo CI/CD integrados directamente en repositorios de GitHub. | Propietaria (SaaS integrando software Open Source) | Web (Ejecutadores en Linux, Windows, macOS) |
| **Mantenimiento y monitorización** | SonarQube | Análisis estático de código para detección de errores de seguridad, *code smells* y vulnerabilidades. | LGPLv3 (Community Edition) | Windows, macOS, Linux (Docker) |

---

## Comparativa de herramientas

### Categoría seleccionada
Herramientas de construcción (*Build tools*).

### Contexto de la elección
Un equipo reducido de 3 desarrolladores de la empresa municipal de informática trabaja en una aplicación Java (JDK 17) para la gestión del Polideportivo Municipal. Cuentan con un presupuesto ajustado, máquinas corporativas estándar y necesitan una curva de aprendizaje rápida sin invertir tiempo excesivo en la configuración de *scripts* complejos de construcción.

---

### Datos recogidos

* **Fecha de consulta**: 04/11/2026

| Criterio / Dato | Apache Maven | Gradle |
|---|---|---|
| **Última versión estable** | 3.9.6 (publicada el 25/11/2023) | 8.5 (publicada el 29/11/2023) |
| **Licencia** | Apache License 2.0 | Apache License 2.0 |
| **Modelo de configuración** | Declarativo en XML (`pom.xml`) | DSL basado en Groovy o Kotlin (`build.gradle` / `build.gradle.kts`) |
| **Rendimiento / Velocidad** | Estándar; compilación secuencial o en paralelo básica por módulos. | Alto; uso intensivo de caché de *build*, compilación incremental y *daemon* persistente. |
| **Curva de aprendizaje** | Baja; estructura de proyecto estándar y rígida ("Convención sobre configuración"). | Media-Alta; requiere aprender sintaxis DSL y lógica de construcción imperativa/declarativa. |
| **Integración con IDEs** | Nativa y completa en Eclipse, IntelliJ IDEA, NetBeans y VS Code. | Completa en IntelliJ IDEA, Eclipse y Android Studio; requiere configuración adicional en otros editores. |
| **Fuentes** | 1. Sitio oficial de Apache Maven: [https://maven.apache.org](https://maven.apache.org)<br>2. Sitio oficial de Gradle: [https://gradle.org](https://gradle.org) | 1. Documentación oficial de Gradle: [https://docs.gradle.org](https://docs.gradle.org)<br>2. Repositorio GitHub de Gradle: [https://github.com/gradle/gradle](https://github.com/gradle/gradle) |

---

### Matriz de decisión

| Criterio | Peso (1-3) | Justificación del peso | Puntuación Maven (1-5) | Puntuación Gradle (1-5) | Total Maven (Peso × Puntuación) | Total Gradle (Peso × Puntuación) |
|---|---|---|---|---|---|---|
| **Facilidad de uso y curva de aprendizaje** | **3** | El equipo es reducido y necesita estar operativo de inmediato sin dedicar días a aprender lenguajes de *scripting*. | 5 | 3 | 15 | 9 |
| **Coste y Licencia** | **3** | Al ser un proyecto municipal con presupuesto restringido, es imperativo utilizar software totalmente libre y gratuito. | 5 | 5 | 15 | 15 |
| **Estandarización y convención** | **2** | Es importante mantener una estructura de proyecto uniforme para que cualquier desarrollador municipal lo entienda. | 5 | 3 | 10 | 6 |
| **Rendimiento en la construcción** | **1** | Al ser una aplicación pequeña/mediana, el tiempo de compilación no es un cuello de botella crítico. | 3 | 5 | 3 | 5 |
| **Integración con IDEs y herramientas CI** | **2** | El entorno debe integrarse sin problemas en la infraestructura básica de desarrollo y repositorios. | 5 | 4 | 10 | 8 |
| **TOTAL** | | | | | **53** | **43** |

*Cálculos comprobados:*
- **Total Maven**: $(3 \times 5) + (3 \times 5) + (2 \times 5) + (1 \times 3) + (2 \times 5) = 15 + 15 + 10 + 3 + 10 = 53$
- **Total Gradle**: $(3 \times 3) + (3 \times 5) + (2 \times 3) + (1 \times 5) + (2 \times 4) = 9 + 15 + 6 + 5 + 8 = 43$

---

### Conclusión

Para el contexto específico de este proyecto se selecciona **Apache Maven**, al haber obtenido la puntuación total más alta (**53 puntos frente a 43**). 

Aunque Gradle ofrece un rendimiento superior en proyectos de gran escala gracias a su caché incremental y *daemon*, en un proyecto municipal de escala media la velocidad de compilación no supone una ventaja crítica. En cambio, la rigidez del modelo declarativo en XML de Maven y su principio de "convención sobre configuración" permiten al equipo de tres desarrolladores empezar a trabajar de forma inmediata, manteniendo una estructura estándar y sin necesidad de mantener complejos scripts de construcción en Groovy o Kotlin.

---

## Preguntas

1. **¿Por qué la licencia de una herramienta es un factor clave en proyectos reales y no basta con saber si es «gratuita»?**  
   Porque «gratis» o *freemium* no implica que el software sea de código abierto ni que autorice el uso comercial o administrativo. Licencias permisivas (como MIT o Apache 2.0) otorgan el derecho legal de modificar, distribuir y ejecutar el código en cualquier entorno sin costes ocultos ni cambios imprevistos en los términos de servicio, garantizando la sostenibilidad legal del proyecto.

2. **¿Qué ocurre cuando un equipo elige una herramienta con una curva de aprendizaje muy alta para un proyecto con un plazo de entrega muy corto?**  
   Se genera un cuello de botella en el calendario: gran parte del tiempo inicial asignado a la entrega de funcionalidades consumibles se desperdicia en la configuración del entorno y en resolver dudas operativas de la herramienta, disparando el riesgo de incumplir las fechas límite comprometidas.

3. **¿En qué situaciones puede ser preferible elegir una herramienta que ha obtenido menor puntuación en la matriz de decisión?**  
   Cuando surgen condicionantes o restricciones externas no cuantificadas en la matriz, como normativas de cumplimiento de seguridad de obligado acatamiento, integración impuesta con sistemas *legacy* de la organización, o si la empresa ya cuenta con licencias y personal cualificado en dicha herramienta dentro de otro departamento.
