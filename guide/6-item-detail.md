# Pagina de detalle de una tarea

En este paso vamos a agregar la pagina de detalle de una tarea.

En este paso, a diferencia del resto, vamos a proveer solamente una lista a alto nivel de las tareas a realizar:

1. Agregar en `index.html` una nueva ruta que apunte a `/item/:uid`
2. Agregar en `<task-card>` un link a cada item parametrizado con su ID de la siguiente forma: `/item/123`. El link debe envolver el `h2`del titulo.
3. Crear la pagina `item-page.html` con el detalle del item. La idea es mostrar el titulo en el header y la descripcion en el contenido.

> **Nota:** El `<task-service>` puede ademas de devolver el listado de tareas, devolver una tarea particular dado un ID. Para eso, debe ser usado de la siguiente forma:

````html
<task-service id="service" uid="uuid a buscar" task="binding de tarea recibida del server"></task-service>
````

Una vez terminada, la pagina de detalle se deberia ver similar a la siguiente:

![detalle](https://cloudup.com/cOPdCP1sM5a+)

Happy hacking :)!
