
# Activity Manager - Component Design



## Goal
El Activity Manager es el **componente encargado de gestionar las actividades**. Tiene acceso a todos los detalles de las actividades del registro y cuando es solicitada una ejecución específica, crea una instancia de la actividad y la arranca.

Todas las actividades consisten en una secuencia de una o varias acciones, llamadas “pasos” que pueden ser parte de otras actividades. Según la terminología empleada por BIC, podemos hablar de **tres tipos de actividades**:

 - *Actividad Contextual*: representa una secuencia de operaciones y eventos que producen una salida, pero no necesita interacción con el usuario. Puede requerir algunos datos de entrada que estarán disponibles como parámetros de actividad o en el contexto de la aplicación. Este tipo de actividades son lanzadas automáticamente desde las actividades de la plataforma, basadas en cambios de estado del Escritorio o la aplicación (p. e. arranque, parada, etc.)
 - *Actividad de Front-End*: es una actividad que modela un caso de negocio. Es una tarea que arranca una o más vistas y tiene interacción con el usuario para conseguir los datos de entrada necesarios y mostrar el resultado de la actividad. Parte de los datos de entrada también pueden provenir del contexto de la aplicación donde se puede haber almacenado el resultado de otras actividades front-end. De la misma manera, la salida de una actividad front-end puede ser añadida al contexto o se puede disparar un evento notificando que un valor ha cambiado. Este tipo de actividades pueden lanzarse desde las actividades de la plataforma, desde otras actividades de aplicación o desde un menú. Las actividades front-end se presentan siempre en un área específica del escritorio (el área de trabajo). Importante referir que la recuperación y persistencia de datos propios de un flujo de negocio quedan afuera del ámbito de una actividad frond-end.
 - *Actividad Ejecutable:* es una actividad que no requiere ni acceso al contexto de la aplicación para compartir datos, ni la interacción de usuario.

## Responsibility 
•	Manejar actividades registradas.

•	Lanzar actividades.

## Relationships

![Component Diagram](http://blog.ibmjstart.net/wp-content/uploads/2015/12/component-diagram.png)


## Design Principles
El componente Activity Manager es necesario para proveer las funcionalidades básicas para integrar las diferentes actividades sobre la AEI.

El Activity Manager consiste en un componente que podrá ser usado desde cualquier componente de la Arquitectura para acceder y controlar todas las actividades que se están ejecutando.

Para que el Activity Manager pueda lanzar y manejar adecuadamente una actividad específica, todas las actividades de aplicación deben seguir una implementación concreta dependiendo del tipo de actividad. Las actividades deben registrarse como actividad de la Arquitectura por medio de un punto de extensión. Del registro de las actividades se encarga el componente “Activity Registry”: este componente proporciona los puntos de extensión que debería usar la aplicación para registrar una nueva actividad o una nueva factoría de actividades. Este es el modo usado por la plataforma para identificar la clase que representa una actividad y que implementa la lógica de la misma. Permite acceder a algunas propiedades de la actividad que controlan el cómo y cuándo una actividad puede ser ejecutada cuando está corriendo sobre el escritorio y define como una actividad debería ser creada e inicializada.
Concretamente para una actividad del tipo front-end se asume que:
•	Requiere interacción con el usuario. Está construida como un conjunto de vistas que aparecerán en el área de trabajo, presentando las distintas tareas necesarias para completar la actividad.
•	Usa el contexto para compartir datos entre las diferentes tareas, para acceder a datos que han sido actualizados por otra actividad o publicar datos que podrían ser usados por cualquier otra actividad.
El subsistema BIC proporciona la interfaz y una implementación por defecto para el Activity Manager y Activity Registry (capa TIL).

## Architectural Decisions

//UPDATE-ME

## Component Specification (use for L3)

###Package Organization

###Interface Descriptions

###Class Descriptions
- Classes
- Attributes (representing the knowledge responsibilities or data)
- Methods (representing operational responsibilities or functions)
- Association relationships between classes
- Aggregation relationships between aggregate and component classes
- Inheritance relationships between superclasses and subclasses

![Class Diagram](http://method.ibm.com/rmchtml_ad_20/core.tech.common.extend_supp-ibm/workproducts/resources/class_diagram.gif)

###Resource Descriptions

---
