# Empecemos!

Vamos a empezar a trabajar con la carpeta `starter`. Abranla con su editor favorito (Yo uso Sublime Text <3). Deberian ver la siguiente estructura de directorios:

````html
polymer-workshop/
  api/          <!-- una API fake para consumir -->
  components/   <!-- Las dependencias ya instaladas por Bower -->
  guide/        <!-- Donde se encuentran las instrucciones de cada paso para realizar este workshop -->
  task-service/ <!-- Un componente que vamos a usar en el workshop -->
  starter/      <!-- El punto del cual vamos a empezar el proyecto! -->
  step-2/       <!-- Checkpoints de cada paso que damos -->
  step-3/
  step-4/
  step-5/
  .bowerrc      <!-- Archivo de configuracion de bower -->
  .gitignore
  bower.json    <!-- El archivo de metadata de bower donde pusimos las dependencias -->
````

Para empezar a trabajar en el proyecto, necesitamos poder servir esta carpeta. Para eso, si tienen `node` instalado, pueden usar `serve` (`npm install -g serve`) o si tienen `python` usar `python -m SimpleHTTPServer`.

Una vez levantado el servidor, vayan a `http://localhost:3000/starter/` y deberian ver algo similar a lo siguiente:

![Start](https://cloudup.com/ci238hBeemc+)

Ahora que ya podemos ver la app, empecemos a codear! [Vamos a empezar haciendo el Layout!](2-layout.md)
