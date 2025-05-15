#### Actividad 4

```js
// Variables globales
let inputValue = 0; // Input: puede venir del mouse, teclado o red
let outputColor;
let socket; // si usas comunicación en red

function setup() {
  createCanvas(600, 400);
  outputColor = color(255);

  // Comunicación por red (si aplica)
  // socket = io.connect("http://localhost:3000");
  // socket.on('inputData', data => {
  //   inputValue = data;
  // });
}

function draw() {
  // PROCESO: modifica el estado basado en el input
  let mappedValue = map(inputValue, 0, 1023, 0, 255);
  outputColor = color(mappedValue, 100, 255 - mappedValue);

  // OUTPUT: visual que refleja el estado
  background(0);
  fill(outputColor);
  ellipse(width/2, height/2, 100 + mappedValue / 2);
}

// INPUT DIRECTO
function mouseMoved() {
  inputValue = mouseX; // por ejemplo, el input ahora es la posición del mouse
}

// INTERACCIÓN DIRECTA
function keyPressed() {
  if (key === 'r') {
    inputValue = 0; // resetea el input
  }
}

```
