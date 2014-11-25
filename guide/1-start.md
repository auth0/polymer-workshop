# Empecemos!

Empezaremos el proyecto con la carpeta `starter`. Si la abren con su editor preferido (Yo uso `Sublime Text` <3), deberian ver la siguiente estructura de directorios:

````
polymer-workshop/
  api/          <!-- una API fake para consumir -->
  components/   <!-- Las dependencias ya instaladas por Bower -->
  guide/        <!-- Donde se encuentran los pasos para realizar este workshop -->
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

Necesitamos servir esta carpeta para empezar a trabajar con el proyecto. Para eso, si tienen `node` instalado, pueden instalar `serve` (`npm install -g serve`) y correr `serve` o hacer `python -m SimpleHTTPServer` si tienen `python`.

Deberian ver algo similar a lo siguiente:

![Start](https://cloudup.com/ci238hBeemc+)

[Continuemos!](2-layout.md)
