# Layout

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

Por ultimo, vemos que estamos usando `<app-router>`, el WebComponent que importamos mas arriba. En este caso, estamos creando la ruta `/home` que apunta a `home-page.html`. Este va a ser el archivo que vamos a modificar en esta primera parte.

## Let's code!

### Agregando los imports

Abramos ahora el archivo `home-page.html` y vamos a ver algo similar a lo siguiente:

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

Aqui estamos ya creando nuestro primer componente. En este componente, vamos a estar utilizando `<core-header-panel>`, `<core-toolbar>` y `<paper-tabs>` para realizar el Layout.  Entonces nuestra **primrea tarea es incluir estos WebComponents que vamos a utilizar**. 

> **Tips:** Estos WebComponent se importan muy similar a Polymer y ya estan bajados en la carpeta `component`

### Haciendo el Layout

Ahora que ya tenemos importados los elementos que vamos a usar es hora de hacer el layout.

**Para eso, vamos a crear un `<core-header-panel>` y ponerle adentro un `<core-toolbar>` y un `<div class="container">`**

> **Tip:** Vimos como hacer un layout similar en los [slides aqui](https://docs.google.com/a/gon.to/presentation/d/1Xyr5LotQUDT9O8sH7Eau5-7SGXwMvys8FR0BjrI8oqo/edit#slide=id.g3a1d4647c_2_554)

Para que el `<core-header-panel>` se vea, nosotros tenemos que settearle un height explicito. Una forma facil de hacer esto es mediante los [layout attributes](https://www.polymer-project.org/docs/polymer/layout-attrs.html) los cuales se basan en Flexbox.

**Ahora, al `<template>` tag le vamos a aclarar que queremos un layout vertical que ocupe todo el viewport y luego al `<core-header-panel>` le tenemos que settear que va a controlar su propio tamaño usando Flexbox**

> **Tip:** Todas las propiedades que tenemos que usar se encuentran en la [documentaction de layouts](https://www.polymer-project.org/docs/polymer/layout-attrs.html)

Ahora ya se deberia ver nuestro Header y nuestro Content:

![Content](https://cloudup.com/ctJlNFQtuls+)

### Agregando los tabs

Ya tenemos ahora nuestro Layout principal. Lo que vamos a hacer ahora es agregar 2 tabs a nuestra toolbar. Uno con todas las tareas a realizar (All) y otro con las tareas que ya procastinamos (Procastinated).

Para eso, vamos a usar los [`<paper-tabs>`](https://www.polymer-project.org/docs/elements/paper-elements.html#paper-tabs). 

**Entonces vamos a crear 2 tabs. Uno deberia decir `all` y el otro `procastinated`**. 

> **Tip:** La implementacion es igual a la de la [documentacion](https://www.polymer-project.org/docs/elements/paper-elements.html#paper-tabs), la unica diferencia es que nosotros para identificar a cada tab vamos a usar la property `name` en vez del indice y `selected` va a apuntar al `name` del primer tab.

Se deberian ver asi:

![image](https://cloudup.com/cyM7EWHgwNU+)

Vamos a ver que los tabs no se expanden al width total de la barra. Para eso tenemos que indicar que los hijos van a controlar su propio espacio y se van a expandir al espacio que les da el padre usando Flexbox. A su vez, tambien queremos que los labels se alinien al final del container

> **Tip:** Ambas properties a usar se encuentra en la documentacion de [layout](https://www.polymer-project.org/docs/polymer/layout-attrs.html) y una la usamos en un ejercicio anterior

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





