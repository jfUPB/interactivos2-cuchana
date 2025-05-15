#### Actividad 6

Muestra un ejemplo significativo de cómo mejoraste la claridad del código:
Puede ser un fragmento donde cambiaste nombres de variables/funciones poco claros por otros más descriptivos (muestra el antes y el después).
O un fragmento donde añadiste comentarios clave que explican una parte compleja (muestra el código comentado).
O un ejemplo de reorganización/simplificación del código.
Reflexiona brevemente sobre la importancia de tener un código limpio y comentado, especialmente de cara a la documentación final y a un posible portafolio.

Profe para responderte a esto adjunto el link con el codigo limpio del prototipo de conexion we y el codigo de p5.js 
Honestamente el limpiar el codigo me ayudo mucho para evitar cometer ciertos errores en la simulacion y tener todo bien organizado, los nombres de las variables corregidos, y asi evito las confusiones con la transmision de los datos y codigos.


https://github.com/cuchana/sfiSocketioDesktopMobile.git

```js
let modeloX;
let pasoIzquierdo = true;
let avanzando = false;
let direccion = 1; // 1 = derecha, -1 = izquierda
let animacionPaso = 0;

let particulas = [];
let coloresGalaxia;

function setup() {
  createCanvas(800, 400);
  modeloX = width / 2;
  frameRate(60);

  coloresGalaxia = [
    color(255, 100, 255, 180),
    color(100, 200, 255, 180),
    color(255, 255, 150, 180),
    color(200, 100, 255, 180)
  ];
}

function draw() {
  background(10, 10, 30);

  // Actualizar partículas galaxia
  for (let i = particulas.length - 1; i >= 0; i--) {
    particulas[i].actualizar();
    particulas[i].mostrar();
    if (particulas[i].tam < 0.5) {
      particulas.splice(i, 1);
    }
  }

  // Animar paso
  if (avanzando) {
    animacionPaso++;
    modeloX += direccion * 2.2;
    if (animacionPaso >= 20) {
      animacionPaso = 0;
      avanzando = false;
    }
  }

  // Dibujar modelo con movimiento
  dibujarModelo(modeloX, height - 80 + sin(frameCount * 0.2) * 2);
}

function keyPressed() {
  if (!avanzando && (keyCode === RIGHT_ARROW || keyCode === LEFT_ARROW)) {
    direccion = keyCode === RIGHT_ARROW ? 1 : -1;
    pasoIzquierdo = !pasoIzquierdo;
    generarGalaxia(modeloX);
    avanzando = true;
  }
}

function generarGalaxia(x) {
  for (let i = 0; i < 40; i++) {
    particulas.push(new ParticulaGalaxia(x, height - 90));
  }
}

class ParticulaGalaxia {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.angulo = random(TWO_PI);
    this.distancia = random(0, 30);
    this.tam = random(2, 6);
    this.velRotacion = random(-0.05, 0.05);
    this.alpha = 200;
    this.color = random(coloresGalaxia);
  }

  actualizar() {
    this.angulo += this.velRotacion;
    this.distancia *= 1.01;
    this.tam *= 0.98;
    this.alpha *= 0.97;
  }

  mostrar() {
    let px = this.x + cos(this.angulo) * this.distancia;
    let py = this.y + sin(this.angulo) * this.distancia;
    fill(red(this.color), green(this.color), blue(this.color), this.alpha);
    noStroke();
    ellipse(px, py, this.tam);
  }
}

function dibujarModelo(x, y) {
  push();
  translate(x, y);

  // Cuerpo
  fill(255);
  rect(10, 0, 20, 40);
  ellipse(20, -10, 25);

  // Piernas
  stroke(255);
  strokeWeight(3);
  let desplazamiento = sin(frameCount * 0.2) * 12;

  if (pasoIzquierdo) {
    line(15, 40, 10 + desplazamiento, 65);
    line(25, 40, 30, 60);
  } else {
    line(15, 40, 10, 60);
    line(25, 40, 30 + desplazamiento, 65);
  }

  // Brazos
  line(10, 10, -5 + sin(frameCount * 0.1) * 5, 30);
  line(30, 10, 45 + cos(frameCount * 0.1) * 5, 30);

  pop();
}
```
