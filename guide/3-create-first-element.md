# Creando nuestro primer WebComponent

Ahora que ya sabemos usar WebComponents existentes y que tenemos terminado el Layout de la aplicacion, podemos crear nuestro primer WebComponent. 

## Creando `<task-card>`

Esta tarjeta tendra los detalles de la tarea a procastinar. Tendra un header con el titulo y luego un texto con la descripcion. Se va a ver asi:

![card](https://cloudup.com/cuwAQahVOY8+)

Y se va a usar de la siguiente forma:

````html
<task-card>
  <h2>Buy the milk</h2>
  <p>Go to the supermarket and buy some milk</p>
</task-card>
````

### Entendiendo la estructura de un WebComponent

Vayamos al archivo `task-card.html`:

````html
<polymer-element name="task-card">
  <template>
    <style>
    :host {
      display: block;
      position: relative;
      background-color: white;
      padding: 20px;
      width: 100%;
      font-size: 1.2rem;
      font-weight: 300;
    }
    .card-header {
      margin-bottom: 10px;
    }
    </style>

  </template>
  <script>
  Polymer({});
  </script>
</polymer-element>
````

Lo primero que vemos es el tag `<polymer-element>`. Este se encarga de crear un WebComponent llamado `task-card`. Para eso usamos la property `name` de este tag. 

Mas abajo vemos el tag `<template>`. Todo lo que vaya dentro de este tag va a ser parte del ShadowDOM de nuestro componente. Esto significa que todo este contenido va a estar isolado del resto.

Luego, dentro del tag `<style>` vemos el pseudo selector `:host`. Este va a seleccionar al elemento que estamos creando, en este caso `<task-card>`. 

Mas abajo vemos el selector `.card-header`. Este _solo_ va a aftectar a los tags con clase `card-header` que se encuentren dentro del WebComponent. 

Por ultimo, en la parte de `<script>`, podemos ver que estamos llamando a `Polymer({})`. Esto registra la `<task-card>` con el Browser para que sea reconocido luego cuando lo insertamos en otro lugar de la pagina.

## Let's code!

### Haciendo el template

Es hora de crear nuestro template! 

Como vimos en la imagen al principio, la idea es tener un header con el titulo de la tarea y luego la descripcion abajo mas pequeña. Para eso, vamos a usar algo que se llama _Insertion points_. Un _Insertion point_ le dice al browser en que lugar de nuestro WebComponent se va a insertar el contenido adicional que fue añadido desde afuera. Si no ponemos ningun insertion point y usamos un WebComponent como `<task-card><h3>Hola</h3></task-card>`, el contenido del H3 nunca sera mostrado por el browser.Estos insertion points se crean con el tag `<content>`.

#### Tarea 1: Crear un div con la clase `card-header` que adentro tenga un insertion point para el `h2` y luego poner otro insertion point por furea del `card-header` para el resto del contenido.
El resultado deberia ser similar al siguiente:

````html
<div class="card-header">
  <!-- Insertion point para el h2 -->
</div>
<!-- Insertion point para el resto del contenido -->
````

> **Tip:** Pueden ver como usar el `<content>` tag [aqui](https://dvcs.w3.org/hg/webcomponents/raw-file/57f8cfc4a7dc/explainer/index.html#shadow-dom-section) en la seccion "Content and Shadow Elements". Prestar especial atencion al atributo `select`.

Ahora, lo que vamos a hacer es darle estilos al componente que acabamos de crear. Para eso, debemos agregar lo siguiente adentro del tag `<style>`

````css
.card-header {
  margin-bottom: 10px;
}
.card-header ::content h2 {
  margin: 0;
  font-size: 1.8rem;
  font-weight: 300;
}
````

Como pueden ver, en este caso estamos utilizando el pseudo selector `::content` para solo darle estilos a elementos dentro de un `<content>`.

### Usando nuestro componente

Hora de usarlo!

#### Tarea 2: Importar el componente recien creado desde la `home-page.html`

#### Tarea 3: Usarlo dentro del `<div class="container">` de la siguiente manera:


````html
<div class="container" layout vertical center>

  <task-card>
    <h2>Buy the milk</h2>
    <p>Go to the supermarket and buy some milk</p>
  </task-card>

</div>
````

Ahora, deberiamos ver algo similar a lo siguiente:

![added web](https://cloudup.com/cSA6K_9ZtMQ+)

> **Nota:** Como una nota interesante, prueben cambiar de lugar el `h2` y el `p` de dentro del `<task-card>` y van a ver que la UI no cambia. Eso es porque nosotros setteamos el orden usando los `<content>` tags.

[Hora de agregar WebServices y DataBinding para mostrar las otras tareas!](4-web-services-data-binding.md)


