# Procastinando tareas

Ya podemos ver el listado de tareas. No obstante, aun hay 2 cosas que debemos cambiar.

1. Necesitamos una forma de procastinar las tareas
1. El listado de tareas es el mismo tanto en el tab `All` como en el `Procastinated`. La idea es que el tab `Procastinated` tenga solamente las tareas Procastinadas.

## Agregando el toggle para procastinar tareas

Lo primero que vamos a hacer es agregar un toggle que permita Procastinar una tarea en la `<task-card>`. 

Para esto, necesitamos poder decirle a la `<task-card>` si la tarea esta procastinada o no y necesitamos poder cambiar el estado de procastinacion de la tarea desde la `<task-card>`. En otras palabras, lo que necesitamos es crear un _2 way binding_ entre la `<task-card>` y `task.procastinated`. Para eso, vamos a usar [published properties](https://www.polymer-project.org/docs/polymer/polymer.html#published-properties).

**Tarea: Publicar la propiedad `procastinated` desde `<task-card>`**

> **Tip:** Podemos ver como publicar propiedades en [este articulo](https://www.polymer-project.org/docs/polymer/polymer.html#published-properties). Hay 2 formas diferentes. Podemos usar cualquiera de las 2!

Una vez publicada la propiedad, podremos acceder a la misma desde el JS via `this.procastinated` o desde el HTML via un binding `{{procastinated}}`.

Ahora ya podemos agregar el `<paper-toggle-button>` que cambiara el valor de `task.procastinated` cuando es clickeado.

**Tarea: Insertar el toggle donde se especifica a continuacion y bindear el atributo `checked` del toggle a la propiedad `procastinated` que nuestro WebComponent esta recibido por parametro.**

````html
<div class="card-header">
  <content select="h2"></content>
</div>
<!-- Insertar toggle aqui -->
<content></content>
````

> **Tip:** La documentacion sobre como usar el `<paper-toggle-button>` se puede encontrar [aqui](https://www.polymer-project.org/docs/elements/paper-elements.html#paper-toggle-button)

Ahora que ya esta implementado, agreguemos el siguiente CSS para que nuestro Toggle se vea mejor:

````css
paper-toggle-button {
  position: absolute;
  top: 30px;
  right: 3px;
  color: #636363;
}
````

Por ultimo, debemos pasar la propiedad `procastinated` desde la `<task-list>` hacia la `<task-card>` de la siguiente forma:

````html
<template repeat="{{task in tasks}}">
  <task-card procastinated="{{task.procastinated}}">
    <h2>{{task.name}}</h2>
    <p>{{task.description}}</p>
  </task-card>
</template>
````

La lista ahora se deberia ver de la siguiente forma:

![list](https://cloudup.com/cYBm3FwELEm+)

## Mostrando las tareas que corresponde por tab

Ahora ya podemos procastinar tareas. Lo que nos falta es que cada tab muestre lo que deberia.

Para eso, **lo primero que vamos a hacer es exponer una propiedad `show` desde nuestro `<task-list>` la cual va a recibir que tareas mostrar** 

> **Tip:** Esto es lo mismo que hicimos en el punto anterior :).

**Luego, desde nuestro `home-page.html` vamos a settear este parametro show al tab actualmente setteado**. Para esto, podriamos usar DataBinding, pero para aprender algo nuevo, vamos a hacerlo mediante eventos.

Polymer tiene muchos [Lifecycle events](https://www.polymer-project.org/docs/polymer/polymer.html#lifecyclemethods). En nuestro caso, una vez que nuestro WebComponent ya se encuentra preparado, vamos a escuchar al evento `core-select` del elemento `<paper-tabs>`, el cual es emitido cada vez que cambia el tab seleccionado. En el handler del event, vamos a settear la property `show` de la lista al nombre del tab seleccionado.

El resultado final de esto es el siguiente codigo.

````js
Polymer({
    ready: function() {
      var tabs = this.$.tabs;
      var list = this.$.list;

      tabs.addEventListener('core-select', function() {
        list.show = tabs.selected;
      });
    }
  });
````

El helper `this.$` nos permite obtener elementos del DOM de forma facil mediante el uso de sus IDs.

Luego, en el `<task-list>` lo que vamos a hacer es ocultar las `<task-card>` cuyas tareas fueron procastinadas si nos encontramos en el tab `procastinated`.

Para eso, vamos a usar la propiedad [`hidden?`](https://www.polymer-project.org/docs/polymer/layout-attrs.html#general-purpose-attributes) que nos provee polymer para facilitarnos settear `display: none` a un elemento basado en una condicion booleana.

**Entonces, ahora debemos completar la expresion de `hidden` basandonos en lo que vale `show` y `task.procastinated`

````html
<template repeat="{{task in tasks}}">
  <task-card 
    procastinated="{{task.procastinated}}"
    hidden?="{{ poner la expresion aca }}">
    <h2>{{task.name}}</h2>
    <p>{{task.description}}</p>
  </task-card>
</template>
````

Entonces, ahora si vamos al tab Procastinated, se deberia ver asi:

![tab procastinated](https://cloudup.com/cLnhdzVtOz5+)

Con esto damos por terminado el Workshop guiado! Ya tenemos una app completamente funcional!

Agregamos un ultimo paso (opcional) no tan guiado para [agregar la pagina de detalle de una tarea](6-item-detail.md)
