#### Activad #9 






```js
function setup() {
  createCanvas(600, 600);
  noLoop();
}

function draw() {
  background(240);

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
