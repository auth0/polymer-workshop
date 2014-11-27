# Usando WebServices y DataBinding

Ya tenemos nuestra `<task-card>` para mostrar la informacion de una tarea creada. Lo que vamos a hacer ahora es obtener una lista de tareas desde un servicio web y luego usar one way data binding para mostrarlas, en otras palabras rendering (en el siguiente ejercicio haremos two-way databinding).

El servicio ya esta creado de antemano y se llama `<task-service>` (lo pueden encontrar en `/task-service/task-service.html`). Este servicio se conecta a una API fake para hacer el request de todas las tareas a realizar. Vamos a usar este servicio desde el element `<task-list>` el cual se encargara de mostrar la lista de tareas.

## Agregando el servicio

Lo primero que vamos a hacer es importar y usar el servicio en nuestra `<task-list>`.

**Tarea 1: Hacer un import al `<task-service>` y luego usarlo de la siguiente manera:**

````html
<task-service id="service" tasks="{{allTasks}}"></task-service>
<!-- Insertar el resto del contenido desde aqui -->
````

Con el `{{}}` estamos creando un DataBinding entre la lista de tareas devueltas por el servicio y una variable de instancia de nuestro WebComponent. Esto quiere decir que ni bien lleguen las listas de tareas del servidor, nosotros vamos a poder acceder a las tareas via `this.allTasks` desde la `<task-list>`.

## Creando el listado de tareas

Ahora que ya obtenemos las tareas del servicio, lo que nos resta hacer es iterar sobre las mismas y mostrarlas. 

**Tarea 2: Mostrar por cada tarea una `<task-card>` con la informacion de su nombre y descripcion. Las propiedas a mostrar de la task son `task.name` y `task.description`. Usar el siguiente template como referencia:**

````html
<div layout vertical center>

  <template repeat="{{task in allTasks}}">
    <!-- Insertar aqui una task card por cada task -->
  </template>

</div>
````

El `repeat` es una instruccion que itera por la lista de tareas. Cada tarea dentro de la lista es asignada a una variable temporal `task`, la cual puede ser usada dentro del `<template>`. En este caso, debemos mostrar los datos de la variable `task` en una `<task-card>`.

> **Tip:** Es necesario primero importar la `<task-card>` y luego usaremos bindings con `{{}}` para mostrar las propiedades de la tarea.

## Mostrando el listado en la home

Lo unico que nos resta hacer ahora es incluir el `<task-list>` en nuestro `home-page.html` y mostrarlo como parte del contenido.

**Tarea 3: Importar el `<task-list>` en nuestro home**

**Tarea 4: Usarlo dentro del `<div class="container">`. Pongamosle de `id` `list` al `<task-list>`**

Ahora, deberiamos ver el siguiente listado de tareas

![result](https://cloudup.com/cG15DAWYgXr+)

[Continuemos agregando una forma de poder procastinar las tareas](5-procastinating-tasks.md).

