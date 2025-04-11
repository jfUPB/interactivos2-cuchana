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
![image](https://github.com/user-attachments/assets/f20a3ba6-e33e-452f-b1e2-c8de48649bf4)

Aplicación potencial: Una posible aplicacion podria ser para musica, sea en aplicaciones o en vivo donde los cuadritos y los tonos reaccionen al ritmo de la musica, o tambien para fondos de pantalla que reaccionen al tipo de actividad que estamos haciendo.

**Ejemplo 2:**

http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_1_2_01

Descripción: Este codigo dibuja una cuadricula de círculos en la pantalla, la cantidad esta dada por tileCount, cada circulito se mueve aleatoriamente segun la posicion del mouse y se puede cambiar la disposicion haciendo click.

Variaciones: cambie el código para que se dibujen cuadrados en vez de circulos, solo renombre las variables, cambie ellipse por rect y cambie la transparencia de los cuadrados.

```js

var tileCount = 20;
var actRandomSeed = 0;

var squareAlpha = 100
var squareColor;

function setup() {
  createCanvas(600, 600);
  noFill();
  squareColor = color(0, 0, 0, squareAlpha);
}

function draw() {
  translate(width / tileCount / 2, height / tileCount / 2);

  background(255);

  randomSeed(actRandomSeed);

  stroke(squareColor);
  strokeWeight(mouseY / 60);

  for (var gridY = 0; gridY < tileCount; gridY++) {
    for (var gridX = 0; gridX < tileCount; gridX++) {

      var posX = width / tileCount * gridX;
      var posY = height / tileCount * gridY;

      var shiftX = random(-mouseX, mouseX) / 20;
      var shiftY = random(-mouseX, mouseX) / 20;

      rect(posX + shiftX, posY + shiftY, mouseY / 15, mouseY / 15);
    }
  }
}

function mousePressed() {
  actRandomSeed = random(100000);
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}


```

Aplicación potencial: Mientras experimentaba con mi variacion noté que hay unos patrones muy interesantes que pueden ser usados para el diseño de camisetas o prendas con este estampado para que los usuarios puedan personalizarla, pueden alterar el color, la transparencia, etc.

**Ejemplo 3:**

Descripción: Este código utiliza p5.js en modo de instancia (var sketch = function(p)) para generar una línea aleatoria con puntos sobre ella. Cada vez que se hace clic, se regenera la forma con una nueva semilla aleatoria, lo que cambia la estructura de la línea y los puntos.

Variaciones: Usar curveVertex() para hacer lineas más curvas y suaves las lineas, y marque mejor los puntos dejando el fill fijo, en vez de random.

```js
var sketch = function(p) {
  var actRandomSeed = 42;

  p.setup = function() {
    p.createCanvas(1024, 256);
  };

  p.draw = function() {
    p.background(255);

    // Línea suavizada con `curveVertex()`
    p.stroke(0, 130, 164);
    p.strokeWeight(1);
    p.strokeJoin(p.ROUND);
    p.noFill();

    p.randomSeed(actRandomSeed);
    p.beginShape();
    p.curveVertex(0, p.height / 2); 
    for (var x = 0; x < p.width; x += 10) {
      var y = p.random(0, p.height);
      p.curveVertex(x, y);
    }
    p.curveVertex(p.width, p.height / 2); 
    p.endShape();

   
    p.noStroke();
    p.fill(0); 

    p.randomSeed(actRandomSeed);
    for (var x = 0; x < p.width; x += 10) {
      var y = p.random(0, p.height);
      p.ellipse(x, y, 4, 4);
    }
  };

  p.mousePressed = function() {
    actRandomSeed = p.random(100000);
  };

  p.keyReleased = function() {
    if (p.key == 's' || p.key == 'S') p.saveCanvas('generative_art', 'png');
  };
};

var myp5 = new p5(sketch);


```


Aplicación potencial: En algun video juego para hacer caminos aleatorios entre niveles.



