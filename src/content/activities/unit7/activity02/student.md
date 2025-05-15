#### Actividad 2

Desktop sketch.js: 
```js
let socket;
let temaActual = "oscuro";
let ultimoTema = null;

let galaxias = [];
let galaxiasFijas = [];
let estrellitas = [];

let imgGalaxia;

function preload() {
  imgGalaxia = loadImage("/galaxia.png");
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();

  socket.on("cambiarTema", (tema) => {
    temaActual = tema;
  });

  socket.on("emitirSonido", (tipo) => {
    galaxias.push(new Galaxia(random(width), random(height), tipo));
  });

  frameRate(60);
}

function draw() {
  fondoGalactico(temaActual);

  for (let g of galaxias) {
    g.actualizar();
    g.dibujar();
  }

  // eliminar galaxias que se desvanecen
  galaxias = galaxias.filter(g => !g.terminada());
}

function fondoGalactico(tema) {
  // solo generamos fondo cuando cambia el tema
  if (tema !== ultimoTema) {
    galaxiasFijas = [];
    estrellitas = [];

    if (tema === "nebulosa") {
      for (let i = 0; i < 20; i++) {
        galaxiasFijas.push({
          x: random(width),
          y: random(height),
          tam: random(100, 200),
          rot: random(TWO_PI)
        });
      }
    } else if (tema === "oscuro") {
      for (let i = 0; i < 100; i++) {
        estrellitas.push({
          x: random(width),
          y: random(height),
          tam: random(1, 3),
          brillo: random(150, 255)
        });
      }
    }

    ultimoTema = tema;
  }

  // dibuja según tema
  if (tema === "nebulosa") {
    background(10, 5, 30);
    for (let g of galaxiasFijas) {
      push();
      translate(g.x, g.y);
      rotate(g.rot);
      imageMode(CENTER);
      image(imgGalaxia, 0, 0, g.tam, g.tam);
      pop();
    }
  } else if (tema === "oscuro") {
    background(0);
    for (let e of estrellitas) {
      noStroke();
      fill(255, e.brillo);
      ellipse(e.x, e.y, e.tam);
    }
  }
}

class Galaxia {
  constructor(x, y, tipo) {
    this.x = x;
    this.y = y;
    this.tamano = 10;
    this.alpha = 255;
    this.tipo = tipo;
  }

  actualizar() {
    this.tamano += 2;
    this.alpha -= 3;
  }

  dibujar() {
    noFill();
    stroke(255, this.alpha);
    ellipse(this.x, this.y, this.tamano);
  }

  terminada() {
    return this.alpha <= 0;
  }
}

```


Mobile sketch.js: 
```js
let socket;

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();

  createButton("Tema: Nebulosa").position(10, 10).mousePressed(() => {
    socket.emit("cambiarTema", "nebulosa");
  });

  createButton("Tema: Oscuro").position(10, 50).mousePressed(() => {
    socket.emit("cambiarTema", "oscuro");
  });

  createButton("BOOM!").position(10, 100).mousePressed(() => {
    socket.emit("emitirSonido", "boom");
  });

  createButton("¡Estallido!").position(10, 140).mousePressed(() => {
    socket.emit("emitirSonido", "explosion");
  });
}

```
