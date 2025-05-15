#### Activad #9 

Enunciado: utilizando p5.js, crea un programa que genere formas geométricas (círculos, cuadrados, triángulos) con posición, tamaño y color aleatorios. Experimenta con diferentes funciones de p5.js para controlar la aleatoriedad y la apariencia de las formas.

Para hacer este código tuve que usar random para el color, tamaño y posicion.

X y Y controla la posicion, que la limite de 0 a 600 que es el tamaño del canva para que no se salgan mucho del borde, y una variable forma que va hasta 3 que cambia entre circulo, cuadrado y triangulo y el tamaño de estas tambien es aleatorio pero limitado.

Nota: el noLoop() es para que no se refresquen los dibujos en cada ejecución


```js
function setup() {
  createCanvas(600, 600);
  noLoop();
}

function draw() {
  background(250);

  for (let i = 0; i < (20,30); i++) {
    let x = random(0,600);
    let y = random(0,600);
    let size = random(20, 100);
    let shapeType = int(random(3)); // 0: círculo, 1: cuadrado, 2: triángulo
    let colores = color(random(255), random(255), random(255));

    fill(colores);
    noStroke();

    if (shapeType === 0) {
      ellipse(x, y, size, size);
    } else if (shapeType === 1) {
      rect(x, y, size, size);
    } else {
      triangle(
        x, y - size / 2,
        x - size / 2, y + size / 2,
        x + size / 2, y + size / 2
      );
    }
  }
}
```
