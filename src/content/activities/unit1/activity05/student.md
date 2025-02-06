#### Actividad #5:

Ejemplo 1: 

http://www.generative-gestaltung.de/2/sketches/?01_P/P_1_2_3_01

Descripción: El sketch genera una cuadrícula de rectángulos con colores aleatorios, los colores se pueden alterar con los numeros de 0 a 9, que cada uno altera la saturacion y brillo de forma aleatoria. Los parametros clave son tileCount (maneja el numero de cuadritos), colorMode(define el modo de color con los numeros).

Usa un arreglo de hueValues, saturationValues y brightnessValues, que almacena los datos de tono, saturacion y brillo, en el setup preestablece un modo de color, quita los bordes y despues le asigna colores aleatorios.
Usan un limitador del mouse dentro de la ventana, evitando que nos salgamos del tamaño del lienzo, el conteo de filas y columnas varia segun la posicion del mouse, y con los numeros generamos nuevos valores de color aleatorios. 

**Variaciones:**

Variacion 1: En la primera variacion aumente el numero de cuadritos e hice que cambiara los colores en funcion al tiempo, elimine las lineas de los numeros y cambie a una funcion de sin y cos, que usa millis para cambiar la iluminacion y la saturación. 

Mantuve todos los valores iniciales, solo cambie el tile count a 50 cada uno, en el draw hice 3 lineas donde se suma un valor basado en una funcion de sin o cos respectivamente para que cambie lentamente el tono de los colores, para la saturacion y el brillo limite los numeros para que esten en un rango armonico visualmente.
```js
var tileCountX = 50;
var tileCountY = 50;

var hueValues = [];
var saturationValues = [];
var brightnessValues = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();

  for (var i = 0; i < tileCountX; i++) {
    hueValues[i] = random(360);
    saturationValues[i] = random(100);
    brightnessValues[i] = random(100);
  }
}

function draw() {
  background(0, 0, 100);

  var mX = constrain(mouseX, 0, width);
  var mY = constrain(mouseY, 0, height);

  var counter = 0;
  var currentTileCountX = int(map(mX, 0, width, 1, tileCountX));
  var currentTileCountY = int(map(mY, 0, height, 1, tileCountY));
  var tileWidth = width / currentTileCountX;
  var tileHeight = height / currentTileCountY;

  for (var gridY = 0; gridY < tileCountY; gridY++) {
    for (var gridX = 0; gridX < tileCountX; gridX++) {
      var posX = tileWidth * gridX;
      var posY = tileHeight * gridY;
      var index = counter % currentTileCountX;

      // Cambio MUY lento en los valores de color
      hueValues[index] = (hueValues[index] + sin(frameCount * 0.0002)) % 360;
      saturationValues[index] = constrain(saturationValues[index] + cos(frameCount * 0.0001) * 0.2, 40, 100);
      brightnessValues[index] = constrain(brightnessValues[index] + sin(frameCount * 0.0001) * 0.2, 50, 100);

      fill(hueValues[index], saturationValues[index], brightnessValues[index]);
      rect(posX, posY, tileWidth, tileHeight);
      counter++;
    }
  }
}
```
https://editor.p5js.org/luciana.gp0531/sketches/mJrG7OYef



Aplicación potencial: Una posible aplicacion podria ser para musica, sea en aplicaciones o en vivo donde los cuadritos y los tonos reaccionen al ritmo de la musica, o tambien para fondos de pantalla que reaccionen al tipo de actividad que estamos haciendo.

**Ejemplo 2:**
http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_1_2_01

Descripción: 

Variaciones: crea al menos dos variaciones, modificando sus parámetros.
Aplicación potencial: describe una posible aplicación de cada ejemplo en el contexto del entretenimiento digital.


