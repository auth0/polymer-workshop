# Creando nuestro primer elemento

Ahora que ya tenemos terminado el Layout de la aplicacion, podemos crear nuestro primer WebComponent. 

Vamos a crear una `<task-card>`. Esta tarjeta tendra los detalles de la tarea a procastinar. Tendra un header con el titulo y luego un texto con la descripcion. Se va a ver asi:

![card](https://cloudup.com/cuwAQahVOY8+)

Y se va a usar de la siguiente forma:

````html
<task-card>
  <h2>Buy the milk</h2>
  <p>Go to the supermarket and buy some milk</p>
</task-card>
````

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

En este archivo, lo primero que estamos haciendo es crear un WebComponent llamado `task-card`. Para eso, usamos el tag `<polymer-element>` especificandole el nombre del componente.

Mas abajo vemos el tag `<template>`. Todo lo que vaya dentro de este tag va a ser parte del ShadowDOM de nuestro componente. Esto significa que todo este contenido va a estar isolado del resto.

Luego, dentro del tag `<style>` vemos el pseudo selector `:host`. Este va a seleccionar al elemento que estamos creando, en este caso `<task-card>`. 

Mas abajo vemos el selector `.card-header`. Este SOLO va a aftectar a los tags con clase `card-header` que se encuentren dentro del WebComponent. Si hay otro `.card-header` en la pagina, este no se vera afectado por el margen setteado.

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


