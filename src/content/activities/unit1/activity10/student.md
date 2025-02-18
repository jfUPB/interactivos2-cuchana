#### Actividad 10:

Vuelve al sitio Generative Design. Selecciona un ejemplo. trata de recrear el ejemplo usando p5.js. PERO, no mires el código. Vas a utilizar una técnica poderosa para aprender llama Deconstruction/Reconstruction propuesta por el profesor Stig Møller Hansen

http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_0_01

Tome de ejemplo este diseño, primero experimente un rato y logré identificar que al mover el mouse en X alteramos el tamaño de la circunferencia, y en Y la cantidad de lineas y su grosor, para construir el código me ayude de chat gpt porque me costó identificar cono definir la función del circulo, sabia que el grosor y la cantidad de líneas las debia definir con map y el radio con X.

```js
function setup() {
  createCanvas(550, 550);
  strokeCap(SQUARE);
}

function draw() {
  background(255);
  translate(width / 2, height / 2);

  let circleResolution = int(map(mouseY, 0, height, 2, 60)); // Cantidad de líneas
  let radius = mouseX - width / 2; // Radio dinámico
  let angle = TWO_PI / circleResolution; 

  strokeWeight(map(mouseY, 0, height, 1, 10)); // Grosor dinámico

  for (let i = 0; i <= circleResolution; i++) {
    let x1 = cos(angle * i) * radius;
    let y1 = sin(angle * i) * radius;
    let x2 = cos(angle * (i + circleResolution / 2)) * radius; 
    let y2 = sin(angle * (i + circleResolution / 2)) * radius;
    
    line(x1, y1, x2, y2); // Dibuja una línea entre dos puntos opuestos
  }
}
```
