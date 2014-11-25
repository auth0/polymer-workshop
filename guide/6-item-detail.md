# Detalles del item

En este paso vamos a agregar la pagina de detalle de una tarea.

A diferencia del resto de los pasos, este no va a ser tan guiado. Lo unico que vamos a proveer es una lista a alto nivel de las tareas a hacer:

1. Agregar en `index.html` una nueva ruta que apunte a `/item/:uid`
2. Agregar en `<task-card>` un link a cada item parametrizado con su ID de la siguiente forma: `/item/123`
3. Crear la pagina `item-page.html` con el detalle del item. La idea es mostrar el titulo en el hader y la descripcion en el contenido.

El `<task-service>` puede ademas de devolver el listado de tareas devolver una tarea particular dado un ID. Para eso, debe ser usado de la siguiente forma:

````html
<task-service id="service" uid="uuid a buscar" task="binding de tarea recibida del server"></task-service>
````

La pagina de detalle se deberia ver similar a la siguiente:

![detalle](https://cloudup.com/cOPdCP1sM5a+)

Con esto damos terminado el workshop.

Muchas gracias!
