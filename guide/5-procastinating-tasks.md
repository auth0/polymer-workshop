# Two Way Data Binding y Publicar Propiedades

Ya podemos ver el listado de tareas. No obstante, aun hay 2 cosas que debemos cambiar.

1. Necesitamos una forma de procastinar las tareas
1. Necesitamos una forma de filtrar tareas para poder mostrarlas en el tab `procastinated`.

## Agregando el toggle para procastinar tareas

Lo primero que vamos a hacer es agregar en la `<task-card>` un toggle que permita Procastinar una tarea. 

Para eso, vamos a usar `<paper-toggle-button>`.

#### Tarea 1: Insertar el toggle donde se especifica a continuacion

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

Ya deberiamos ver el Toggle en nuestra pagina ahora:

![with toggle](https://cloudup.com/c4rqhjg4efP+)

Sin embargo, al cambiar el toggle nada cambia. Necesitamos que cuando se cambie el toggle, cambie el valor de `procastinated` de la tarea. A su vez, el Toggle deberia empezar en ON si una tarea esta `procastinated`. Para esto, necesitamos poder decirle a la `<task-card>` si la tarea esta procastinada o no y necesitamos poder cambiar el estado de procastinacion de la tarea desde la `<task-card>`. En otras palabras, lo que necesitamos es crear  _2 way data binding_ entre la `<task-card>` y `task.procastinated`. Para eso, vamos a usar [published properties](https://www.polymer-project.org/docs/polymer/polymer.html#published-properties).

#### Tarea 2: Publicar la propiedad `procastinated` desde `<task-card>`

> **Tip:** Podemos ver como publicar propiedades en [este articulo](https://www.polymer-project.org/docs/polymer/polymer.html#published-properties). Hay 2 formas diferentes. Podemos usar cualquiera de las 2!

Una vez publicada la propiedad, podremos acceder a la misma desde el JS via `this.procastinated` o desde el HTML via `{{procastinated}}`.

Ahora debemos bindear el estado del toggle con la propiedad `procastinated` que estamos recibiendo.

## Tarea 3: Bindear el atributo `checked` del toggle a la propiedad `procastinated` que nuestro WebComponent esta recibiendo por parametro.

> **Tip:** La documentacion sobre como usar la property `checked` del `<paper-toggle-button>` se puede encontrar [aqui](https://www.polymer-project.org/docs/elements/paper-elements.html#paper-toggle-button)

#### Tarea 4: Por ultimo, debemos pasar la propiedad `procastinated` desde la `<task-list>` hacia la `<task-card>`

> **Tip:** El codigo se deberia ver de la siguiente forma:

````html
<!-- task-list.html -->
<template repeat="{{task in tasks}}">
  <task-card procastinated="{{task.procastinated}}">
    <h2>{{task.name}}</h2>
    <p>{{task.description}}</p>
  </task-card>
</template>
````

La lista ahora se deberia ver de la siguiente forma:

![list](https://cloudup.com/cYBm3FwELEm+)

## Filtrando las tareas procastinadas para el tab `procastinated`

Ahora ya podemos procastinar tareas. Lo que nos falta es que el tab `all` muestre todas las tareas y que el tab `procastinated` muestre solo las tareas procastinadas.

Para eso, lo primero que vamos a hacer es publicar la propiedad `show` en nuestro `<task-list>`. Esta propiedad sera enviada desde la `home-page.html` con el nombre del tab siendo mostrado actuamente (`all` o `procastinated`).

#### Tarea 5: Publicar la propiedad `show` en la `<task-list>`

> **Tip:** Es lo mismo que hicimos cuando publicamos la propiedad `procastinated`.

Luego, desde nuestro `home-page.html` vamos a asignar el valor de `show` en la `<task-list>`. 

> **Nota:** Para esto, podriamos usar data binding pero vamos a usar eventos para aprender algo nuevo.

Cada component creado con Polymer tiene muchos [lifecycle events](https://www.polymer-project.org/docs/polymer/polymer.html#lifecyclemethods). Desde el momento en que un WebComponent es creado hasta el momento en que es removido del DOM, podemos hookearnos a cualquier lifecycle event para agregar comportamiento. En nuestro caso, una vez que nuestro WebComponent ya se encuentra preparado, vamos a escuchar al evento `core-select` del `<paper-tabs>`, el cual es emitido cada vez que cambia el tab seleccionado. En el handler del event, vamos a asignar la property `show` de la lista al nombre del tab seleccionado:

#### Tarea 6: Agregar entonces el siguiente codigo en la `home-page.html` para poder escuchar el evento del cambio de tab

````js
<!-- home-page.html -->
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

Aqui vemos que no solo podemos asignar las _published properties_ via atributos del tag HTML, sino tambien desde el codigo JS.

El helper `this.$` nos permite obtener elementos del ShadowDOM de forma facil mediante el uso de sus IDs. Por ejemplo, con `this.$.tabs` estamos obteniendo el elemento del ShadowDOM cuyo `id` es `tabs`.

Luego, en el `<task-list>` debemos ocultar aquellas tareas que no fueron procastinadas si estamos mostrando el tab `procastinated`.

Para eso, vamos a usar la propiedad [`hidden?`](https://www.polymer-project.org/docs/polymer/layout-attrs.html#general-purpose-attributes) que nos provee Polymer. El atributo `hidden?` nos permite asignar `display: none` a un elemento basado en una condicion booleana.

#### Tarea 7: Completar la expresion de `hidden` basandonos en lo que vale la variable `show` y `task.procastinated`

> **Hint**. Podes hacer cosas asi `a == 'foo' && somethingelse` dentro de una expresion.

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

Ahora si vamos al tab Procastinated, deberia verse asi:

![tab procastinated](https://cloudup.com/cLnhdzVtOz5+)

## Conclusiones

Con esto damos por terminado el Workshop guiado. En este Workshop creamos varios WebComponents diferentes y los hicimos interactuar entre si.

Ante cualquier duda que tengan cuando empiecen a jugar mas con Polymer, pueden mandar un email a [gonto@auth0.com](mailto:gonto@auth0.com) o a [cristian@auth0.com](mailto:cristian@auth0.com).

## Quiero mi remera!

#### Tarea 8: Para ganar tu remera de Auth0 tenes que twittear algo similar a lo siguiente:

````
Polymer workshop with @mgonto and @cristandouce from @auth0 was [disastrous|really bad|meh|nice|great|awesome|outstanding] #jsconfar -> https://github.com/auth0/polymer-workshop
````

## Extra Extra

Si te quedaste con ganas de mas, agregamos un ultimo paso (_opcional_) en el cual tendran que [agregar la pagina de detalle de una tarea](6-item-detail.md). Este paso tiene indicaciones de mas alto nivel para que puedan probar todo lo que aprendieron :).
