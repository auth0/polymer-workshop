# Usando WebServices y DataBinding

Ya tenemos nuestra task card creada para mostrar tareas. Lo que vamos a hacer ahora es obtener una lista de tareas desde un servicio web y luego usar data binding para mostrarlos.

Para eso, nosotros ya hemos creado un servicio llamado `<task-service>`. Este servicio se conecta a una API fake para hacer el request de todas las tareas a realizar. Vamos a usar este servicio desde el element `<task-list>` el cual se encargara de mostrar la lista de tareas.

## Agregando el servicio

Lo primero que vamos a hacer es agregar el servicio a nuestra `<task-list>`.

Para eso, **primero tenemos que hacer un import del `<task-service>`**.

Luego, **lo usaremos de la siguiente manera**:

````html
<task-service id="service" tasks="{{tasks}}"></task-service>
````

Con el `{{}}` estamos creando un DataBinding entre la lista de tareas devueltas por el servicio y una variable de instancia de nuestro elemento. Esto quiere decir que ni bien lleguen las listas de tareas del servidor, nosotros vamos a poder acceder a ellas via `this.tasks`

## Creando el listado de tareas

Ahora que ya obtenemos las tareas del servicio, lo que nos resta hacer es iterar sobre la lista y mostrarlas. **Usando el siguiente template, ahora por cada tarea tenemos que mostrar una `<task-card>`**. Las propiedas a mostrar de la tarea son `task.name` y `task.description`.

````html
<div layout vertical center>

  <template repeat="{{task in tasks}}">
    <!-- Insertar aqui una task card por cada task -->
  </template>

</div>
````

Lo que estamos haciendo aca es iterando por la lista de tareas. Cada tarea dentro de la lista la asignamos a la variable `task`. Luego, usamos esta `task` para mostrar los datos de la `<task-card>`.

> **Tip:** Es necesario primero importar la `<task-card>` y luego usaremos binding con `{{}}` para mostrar las propiedades de la tarea

## Mostrando el listado en la home

**Lo unico que nos resta hacer ahora es incluir el `<task-list>` en nuestro `home-page.html` y mostrarlo como parte del contenido.

El resultado se deberia ver asi:

![result](https://cloudup.com/cG15DAWYgXr+)

[Ahora continuemos agregando una forma de poder procastinar las tareas](5-procastinating-tasks.md).

