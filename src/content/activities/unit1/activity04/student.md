#### Actividad #4 

**Ejemplo 1:** 

Kunst 1 by KodeSkolen:

https://openprocessing.org/sketch/906922

- Descripción del código: El codigo original es super sencillo tenemos un canva, con un fondo gris, y en draw tenemos que el trazo del mouse dibuje elipses blancas.
```js
    function setup() {
  	createCanvas(windowWidth, windowHeight);
  	background(100, 100, 100);
  }
  
  function draw() {
  	ellipse(mouseX, mouseY, 100, 100);
  	fill(255, 255, 255);
  	
  }	
```

Modificación del código: Quise cambiarle la forma, cambiar la elipse por un corazon y dar la opcion de escoger un color, con las teclas R(rojo), G (verde) B (azul) Y P (rosado), como implemente cambio de color decidi mejor cambiar el trazo a que siga la posicion del mouse cuando haga click

```js
let colors = [
  { r: 255, g: 0, b: 0 },     // Rojo
  { r: 0, g: 255, b: 0 },     // Verde
  { r: 0, g: 0, b: 255 },     // Azul
  { r: 255, g: 255, b: 0 },   // Amarillo
  { r: 255, g: 105, b: 180 }, // Rosa
];

let currentColorIndex = 0; // color actual

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(100, 100, 100);
}

function draw() {
  // Solo dibuja corazones cuando el mouse está presionado
  if (mouseIsPressed) {
    fill(colors[currentColorIndex].r, colors[currentColorIndex].g, colors[currentColorIndex].b);
    stroke(0);       // Contorno negro
    drawHeart(mouseX, mouseY, 50);  // Tamaño del corazón
  }
}

// Función para dibujar un corazón en una posición específica, la recicle de un ejercicio de sfi1 
function drawHeart(x, y, size) {
  beginShape();
  vertex(x, y);
  bezierVertex(x - size / 2, y - size / 2, x - size, y + size / 3, x, y + size);
  bezierVertex(x + size, y + size / 3, x + size / 2, y - size / 2, x, y);
  endShape(CLOSE);
}

function keyPressed() {
  // Cambiar el color con las teclas R, G, B, Y, P
  if (key === 'R' || key === 'r') currentColorIndex = 0; // Rojo
  if (key === 'G' || key === 'g') currentColorIndex = 1; // Verde
  if (key === 'B' || key === 'b') currentColorIndex = 2; // Azul
  if (key === 'Y' || key === 'y') currentColorIndex = 3; // Amarillo
  if (key === 'P' || key === 'p') currentColorIndex = 4; // Rosa
}
```
![image](https://github.com/user-attachments/assets/20d0b9ed-6582-4142-9ff7-b6e6db7d5964)


**Ejemplo 2:**
Descripción del código: describe brevemente la funcionalidad del código y los elementos generativos que utiliza (formas, colores, movimiento, etc.).

Modificación del código: realiza al menos dos modificaciones al código original, experimentando con diferentes parámetros y observando los cambios en el resultado visual. Documenta cada modificación y su efecto.

Reflexión: ¿Qué has aprendido sobre el código generativo a través de esta exploración?
