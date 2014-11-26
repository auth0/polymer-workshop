# Usando Polymer Core Components

## Configurando el Layout

### Configurando el index.html

En este paso, lo que vamos a hacer es crear el layout basico de la aplicacion usando componentes Polymers ya existentes.

Dentro de la carpeta `starter`, si vamos al archivo `index.html` veremos algo como lo siguiente:

````html
<!doctype html>
<html>
<head>
  <title>Procastination app</title>

  <meta name="viewport" content="width=device-width, minimum-scale=1.0, initial-scale=1.0, user-scalable=yes">

  <script src="../components/webcomponentsjs/webcomponents.js"></script>

  <link rel="import" href="../components/app-router/app-router.html">

  <link rel="import" href="../components/font-roboto/roboto.html">
<!-- ... -->
</head>
<body unresolved>
  <app-router>
    <app-route path="/home" import="./home-page.html"></app-route>
<!-- ... -->
````

Aqui, estamos primero importando `webcomponent.js`, el cual es el polyfill que permite que usemos WebComponents en browsers que aun no los soportan de forma nativa. Es importante que importemos este script primero, antes que cualquier otro WebComponent.

Luego, estamos incluyendo nuestros primeros 2 WebComponents. El primero sera el Router que usaremos en la aplicacion. El segundo nos importa la Google Web Font `Roboto`.

Vemos que el body tiene el atributo [`unresolved`](https://www.polymer-project.org/articles/styling-elements.html#preventing-fouc). Este atributo hace que el body solo se muestre cuando los WebComponents fueron cargados exitosamente. Si no lo incluyeramos, se veria contenido extraño mientras carga la pagina.

Por ultimo, vemos que estamos usando `<app-router>`, el WebComponent que importamos mas arriba. En este caso, estamos creando la ruta `/home` que apunta a `home-page.html`, el cual va a ser el archivo que vamos a modificar en esta primera parte.

## Let's code!

### Agregando los imports

Abramos ahora el archivo `home-page.html`:

````html
<link rel="import" href="../components/polymer/polymer.html">

<polymer-element name="home-page">
  <template>
    <style>
      ...
    </style>

  <script>
  Polymer({});
  </script>
</polymer-element>
````

Este componente representa a la pagina Home. Vamos a estar utilizando `<core-header-panel>`, `<core-toolbar>` y `<paper-tabs>` para realizar el Layout de esta pagina.

**Tarea: Incluir estos WebComponents que vamos a utilizar**. 

> **Tip:** Estos WebComponent se importan de la misma forma que Polymer y se los puede encontrar en la carpeta `components`. El nombre del archivo a importar es por standard siempre el mismo que el del WebComponent. Por ejemplo `<link rel="import" href="../components/some-component/some-component.html">`

> **Nota:** Como vemos aqui, la `home-page` es un WebComponent. No obstante, explicaremos mas acerca de como crearlos en el siguiente paso. 

### Usando los WebComponents importados

Ahora que ya tenemos importados los elementos que vamos a usar es hora de hacer el layout.

**Tarea: Crear primero un `<core-header-panel>`. Adentro de este vamos a crear un `<core-toolbar>` y un `<div class="container">`**

> **Tip:** Vimos como hacer un layout similar en [estos slides](https://docs.google.com/a/gon.to/presentation/d/1Xyr5LotQUDT9O8sH7Eau5-7SGXwMvys8FR0BjrI8oqo/edit#slide=id.g3a1d4647c_2_554)

Para que el `<core-header-panel>` sea visible en el layout es necesario asignarle un height especifico. Una forma facil de hacer esto es mediante los [layout attributes](https://www.polymer-project.org/docs/polymer/layout-attrs.html), los cuales se basan en [Flexbox](http://css-tricks.com/snippets/css/a-guide-to-flexbox/).

**Tarea: Al `<template>` tag le tenemos que especificar que queremos un layout vertical que ocupe todo el viewport. Luego, al `<core-header-panel>` le tenemos que asignar que va a controlar su propio tamaño usando Flexbox**

> **Tip:** Prestar especial atencion a las propiedades `layout`, `horizontal`, `vertical` y `flex`.

Ahora ya se deberia ver nuestro Header y nuestro Content diferenciados:

![Content](https://cloudup.com/ctJlNFQtuls+)

### Agregando los tabs

Ya tenemos ahora nuestro Layout principal finalizado. Lo que vamos a hacer ahora es agregar 2 tabs a nuestra toolbar. Uno con todas las tareas a realizar (All) y otro con las tareas que ya procastinamos (Procastinated).

Para eso, vamos a usar los [`<paper-tabs>`](https://www.polymer-project.org/docs/elements/paper-elements.html#paper-tabs), los cuales heredan de [`<core-selector>`](https://www.polymer-project.org/docs/elements/core-elements.html#core-selector). 

**Tarea: Crear 2 tabs. El primero deberia decir `all` y el otro `procastinated`**. 

> **Tip1:** La implementacion es similar a la de la [documentacion de `<paper-tabs>`](https://www.polymer-project.org/docs/elements/paper-elements.html#paper-tabs)

> **Tip2:** Nosotros para seleccionar el tab seleccionado usaremos la property `name` en vez del indice. La implementacion deberia ser similar a:

````html
<paper-tabs selected="pepe">
  <paper-tab name="pepe">Pepe</paper-tab>
  <paper-tab name="juan">Juan</paper-tab>
</paper-tabs>
````

El resultado final deberia verse asi:

![image](https://cloudup.com/cyM7EWHgwNU+)

Como vemos en la imagen, los tabs no se expanden al width total de la toolbar y la barrita amarilla no esta alineada con el borde final del container. Vamos a arreglar eso!

**Tarea: Indicar en `<paper-tabs>` que este elemento va a controlar su propio espacio y se va a expandir a todo el espacio provisto por el padre usando Flexbox. A su vez, tambien debemos indicar que se va a alinear al final del container.**

> **Tip:** Ambas properties a usar se encuentra en la documentacion de [layout](https://www.polymer-project.org/docs/polymer/layout-attrs.html). Prestar especial atencion a `self-end` y `flex`.

Ahora, se deberia ver mucho mejor:

![image better](https://cloudup.com/cw2l4W8eK-e+)

Por ultimo, vamos a agregarle estilo a nuestros tabs. En el area de `<style>` agregaremos lo siguiente:

````css
core-toolbar {
  background: #03a9f4;
  color: white;
}
#tabs {
  width: 100%;
  margin: 0;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  text-transform: uppercase;
}
````

Ahora nuestros tabs deberian ser mucho mas lindos:

![tabs](https://cloudup.com/ck4hF90JoZZ+)

Ya con esto tenemos terminado nuestro Layout principal de la aplicacion, pasemos al [proximo paso donde crearemos nuestra task card](3-create-first-element.md)





