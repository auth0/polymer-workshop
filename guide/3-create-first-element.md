# Creando nuestro primer elemento

Ahora que ya tenemos terminado el Layout de la aplicacion, podemos crear nuestro primer WebComponent oficial. 

Lo que vamos a crear es una "Task card", la cual tendra los detalles de la tarea a realizar. Se va a ver asi.

![card](https://cloudup.com/cM5kcjReZWT+)

Y se va a usar de la siguiente forma:

````html
<task-card>
  <h2>Buy the milk</h2>
  <p>Go to the supermarket and buy some milk</p>
</task-card>
````

Si vamos al archivo `task-card.html` vamos a ver que tenemos lo siguiente:

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

En este archivo, primero estamos creando el WebComponent llamado `task-card` con `<polymer-element>`. Luego, todo lo que vaya dentro de `<template>` va a ser parte del ShadowDOM y por ende va a estar isolado del resto.

El pseudo selector `:host` va a seleccionar al elemento que estamos creando, en este caso `<task-card>`. 

Luego, el selector `.card-header` SOLO va a aftectar al contenido de este WebComponent. Si hay otro `.card-header` en la pagina, este no se vera afectado por los cambios.

Por ultimo, en la parte de `<script>`, podemos ver que estamos llamando a `Polymer({})`, lo cual registra este elemento con el Browser para que sea reconocido luego cuando lo insertamos en otro lugar de la pagina.

## Let's code!

### Haciendo el template

Es hora de crear nuestro template! Como vieron en el ejemplo al principio, la idea con este elemento es poder tener un header con el titulo de la tarea y luego el body con la descripcion. Para eso, vamos a usar algo que se llama "Insertion points". Un "Insertion point" le dice al browser en que lugar de nuestro WebComponent se va a insertar el contenido adicional que fue añadido desde afuera. Estos insertion points se crean con el tag `<content>`.

Entonces, lo que vamos a hacer es **crear un div con la clase `card-header` que adentro tenga un insertion point para el `h2` y luego poner otro insertion point por furea del `card-header` para el resto de los elementos agregados. Algo similar a lo siguiente:

````html
<div class="card-header">
  <insertion point para h2>
</div>
<insertion point>
````

> **Tip:** Pueden ver como usar el `<content>` tag [aqui](https://dvcs.w3.org/hg/webcomponents/raw-file/57f8cfc4a7dc/explainer/index.html#shadow-dom-section) en la seccion "Content and Shadow Elements"

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

Como pueden ver, en este acso estamos utilizando el pseudo selector `::content` para solo darle estilos a elementos dentro de un `<content>`

### Usando nuestro componente

Ahora debemos **primero importar el componente recien creado en el `home-page.html` y luego usarlo dentro del `<div class="container">` de la siguiente manera**:


````html
<div class="container" layout vertical center>

  <task-card>
    <h2>Buy the milk</h2>
    <p>Go to the supermarket and buy some milk</p>
  </task-card>

</div>
````

Deberiamos tener ahora algo como lo siguiente:

![added web](https://cloudup.com/cSA6K_9ZtMQ+)

> **Nota:** Como una nota interesante, prueben cambiar de lugar el `h2` y el `p` de dentro del `<task-card>` y van a ver que la UI no cambia. Eso es porque nosotros setteamos el orden usando los `<content>` tags.

[Continuemos ahora usando WebServices y Data Binding](4-web-services-data-binding.md)


