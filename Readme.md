![header_image](image/header.png)

## Desarrollo de una aplicación de productividad con Pomodoro :iphone:

Este proyecto fue desarrollado para el curso de [_Desarrollo de aplicaciones multiplataforma_][enlace_curso] del turno vespertino.

<pre><img src="https://cpilosenlaces.com/wp-content/uploads/2023/03/cpifp-los-enlaces-2x.png" width="200" height="" alt="logo de cpifp los enlaces"> 
</pre>

### <center>Autor</center>

<center>Aura</center>

### <center>Tutor</center>

<center>Rufino</center>

---


> Enfocabita es una aplicación de **productividad** que combina el seguimiento de **habitos** diarios con un temporizador pomodoro, para optimizar la gestión del tiempo :watch:.

---

Nuestros principales _**objetivos**_ al desarrollar esta aplicación son:

- Permitir crear y clasificar los habitos en tres _categorias_: Habitos que se desean mantener, adquirir y abandonar.
- Visualizar el _progreso_ a traves de un calendario.
- Que el usuario pueda consultar su _racha_ de habitos cumplidos.
- _Recordatorios_ para realizar los habitos.
- Gestionar sesiones de trabajo enfocadas, con la ayuda de un temporizador _Pomodoro_.

---

    Antes de iniciar el desarrollo del proyecto, realizamos estudios para determinar el diseño y estructura que tendria la aplicación, no solo en su comportamiento, si no el funcionamiento general al estar en ejecución.

---

Las actividades que realizamos para completar el desarrollo fueron las siguientes:

1. Determinar los recursos y herramientas a utilizar:

   - Elegir recursos software y hardware para crear la aplicación como:

     ![Android Studio](https://img.shields.io/badge/android%20studio-346ac1?style=for-the-badge&logo=android%20studio&logoColor=white) ![Gradle](https://img.shields.io/badge/Gradle-02303A.svg?style=for-the-badge&logo=Gradle&logoColor=white) ![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white) ![Figma](https://img.shields.io/badge/figma-%23F24E1E.svg?style=for-the-badge&logo=figma&logoColor=white) ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white) ![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)

   - Analizar que lenguajes se ajustaban adecuadamente a los requisitos del proyecto. Al ser pensada como una aplicación android, se decidio implementar:

     ![Kotlin](https://img.shields.io/badge/kotlin-%237F52FF.svg?style=for-the-badge&logo=kotlin&logoColor=white) ![Markdown](https://img.shields.io/badge/markdown-%23000000.svg?style=for-the-badge&logo=markdown&logoColor=white) ![XML](https://img.shields.io/badge/XML-ffffff?style=for-the-badge&color=1bb11d)

2. Diseñar diagramas de estructura, flujo e información:
    
   - <u>Diagrama de clases</u>


```Mermaid

erDiagram
    USUARIO {
        int idUsuario
        string nombre
        string correo
        string password
        registrar()
        iniciarSesion()
    }
    HABITO {
        int idHabito
        string nombre
        string categoria
        string frecuencia
        crearHabito()
        editarHabito()
        eliminarHabito()
        vacio
    }
    SesionPomodoro {
        int idSesion
        int idDuracion
        string estado
        date fecha
        iniciarSesion()
        finalizarSesion()
    }
    CALENDARIO {
        Date fecha
        list habitosAociados
        string estado
        visualizarHabitos()
        vacio
    }
    USUARIO ||--o{ HABITO : "tiene"
    USUARIO ||--o{ SesionPomodoro : "asociado"
    CALENDARIO }o--o{ HABITO : "puede tener"
    SesionPomodoro }o--o{ CALENDARIO : "registra"

```

-   <u>Diagrama de caso de usos</u>

```Mermaid

sequenceDiagram

    actor User as Usuario
    participant FE as Frontend
    participant BE as Backend
    participant DB as Base de Datos

    User ->> FE: Abre la aplicación
    FE ->> User: muestra pantalla de inicio
    User ->> FE: solicitud para registrar un hábito
    FE ->> BE: Envia los datos del nuevo hábito registrado
    BE ->> DB: Guarda los datos en la BBDD
    DB -->> BE: Confirma el registro de los nuevos datos
    BE -->> FE: Respuesta de gurdado completo o error
    FE -->> User: Mensaje de confirmación

```

-   <u>Diagrama de flujo</u>

```Mermaid

flowchart TD

    A[Inicio] --> B{Escribe tu contraseña}
    B --> C((pass))
    C --> D{¿Contraseña correcta?}
    D -- Sí --> E[Login correcto]
    D -- No --> F[Intentar de nuevo]
    F --> B
    E --> I[Solicitar duración de sesión]
    I --> S{Confirmar Inicio}
    S -->|Tiempo terminado| N[Notificar fin de sesión]
    S -->|Tiempo restante| Ejecucion[Ejecución de temporizador]
    N --> R[Registrar sesión]
    R --> Fn([Fin])
    S -- No --> Fn


```

3. Analisis y diseño del sistema:

Una vez que determinamos la parte estructural del proyecto, faltaba por analizar el uso de las herramientas y lenguajes antes de la codificación.

Para seguir los estandares actuales del desarrollo de Android y las recomendaciones de Gooogle, decidimos implementar Kotlin para la codificacion y Android studio como entorno de desarollo. En el caso del diseño de la aplicación, al implementar este IDE se utilizara XML como lenguaje de marcado.

Como dato adicional, antes de iniciar la codificacion y desarollo del proyecto, realizamos una serie de cursos para potenciar nuestras habilidades. Los recursos a los que acudimos fueron los siguientes:

   - _Curso de kotlin_  

[![web](https://camo.githubusercontent.com/5c4776adb8c2fb72d3eaac82a756b87b76675628ea957be3d0ba99daae4b01b8/68747470733a2f2f692e696d6775722e636f6d2f6e4444703152612e6a7067)](https://www.youtube.com/watch?v=k9NndvHyUvw&list=PLU8oAlHdN5BkdfBPpNv_lVCJxJgE87cr0)

  - _[Curso de SQL de PildorasInformaticas](https://www.pildorasinformaticas.es/course/curso-sql/)_
  
  - _[Curso de Android Studio Intermedio][enlace_curso_android_studio]_
  
  - _[Curso de Room y Retrofit][enlace_curso_room]_
  

4. Analisis de riesgo:

Por supuesto, antes de irnos de lleno con el proyecto, habia que tomar en cuenta las fortalezas y debilidades que llegaria a tener, es debido a esto que realizamos un analisis DAFO.

| **Fortalezas** | **Oportunidades** |
| -------------- | ----------------- |
| - Desarrollo multiplataforma. | - Alta demanda de aplicaciones de productividad. |
| - Diseño intuitivo, minimalista y simple. | - Integración con tecnologías emergentes. |
| - Personalización del temporizador. | - Potencial para añadir funciones premium. |

| **Debilidades** | **Amenazas** |
| --------------- | ------------ |
| - Limitado presupuesto y recursos. | - Alta competencia en el mercado. |
| - Dependencia de ciertas tecnologías. | - Riesgos de fallas técnicas. |
| - Poco tiempo de desarrollo. | - Posible rechazo de usuarios conservadores. |

5. Implementación:
   
   Este fue el momento donde tocaba empezar a codificar la aplicación e ir adjuntando las clases y metodos a implementar. Para llevar un control mas claro, creamos un diagrama de git y de esa forma ir siguiendo un camino claro.

    ```Mermaid

   gitGraph
   commit id: "Configuracion inicial"
   branch develop
   commit id: "Primer commit en develop"
   branch feature/login
   commit id: "Implementación inical del login"
   commit id: "Validación de credenciales"
   checkout develop
   commit id: "Corrección de errores en los metodos"
   merge feature/login tag: "Merge de login"
   branch feature/UI
   commit id: "Mejora en el diseño de la interfaz"
   checkout develop
   commit id: "Actualización de dependencias"
   merge feature/UI
   branch release/v1.0
   commit id: "Configuración para lanzamiento v1.0"
   checkout main
   merge release/v1.0 tag: "Lanzamiento versión 1.0"
   commit id: "Hotfix: parche para correcion de errores"
   branch hotfix/patch
   commit id: "Correcciones de vulnerabilidades encontradas"
   checkout main
   merge hotfix/patch tag: "Versión 1.0.1"
   commit id: "Actualizacion de funcionalidades"

6. Pruebas
7. Lanzamiento



[enlace_curso_android_studio]: [https://youtu.be/UaR7GSNACsM?si=APX4TGHfb0qKQMJV]

[enlace_curso_room]: [https://www.youtube.com/watch?v=pMqHcrU5w80&list=PL_z8ReaP-3kSZDH645gZtONyyyXfM0gQp]

[enlace_curso]: (https://www.todofp.es/que-estudiar/familias-profesionales/informatica-comunicaciones/des-aplicaciones-multiplataforma.html)