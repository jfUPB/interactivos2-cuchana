#### Actividad 3: 

- Describe la aplicación que propones.
  
  Quiero hacer un tipo de canal de videollamadas donde se comparta un canva que cumpla la funcion de tablero, entonces todo lo que dibujo se ve en la pantalla de ambos clientes.
  Vamos a tener entradas de video, audio y datos al tiempo.
  
- Describe cómo la aplicación propuesta hace uso de la biblioteca p5LiveMedia.

  Para el audio y la camára usamos CAPTURE, se comparte a traves del servidor de señalizacion, el tablero usa DATA, que envia cada trazo en formato JSON (coordenadas, color y grosor), entonces si, usamos el p5LiveMedia para obteneer y compartir estos datos de forma directa.
   
- - Describe cómo la aplicación propuesta se relaciona con el proyecto de curso.
 
    Aunque yo no tengo claro como quiero hacer mi proyecto final del curso, se que todo esto me puede servir para manejar mejor la conexion de clientes y el intercambio de datos entre ellos, ademas me dio una posibilidad que es usar video en vivo y manipularlo en vivo, el proyecto de curso en si es hacer una aplicacion de arte o diseño generativo con todos los conceptos adquiridos, entonces el usar camara, video y datos simultaneamente entre 2 clientes me ayuda a manejar eventos en tiemo real.
    
- Escribe un tutorial que permita replicar la aplicación propuesta.
  Paso 1: Debemos incluir las bibiliotecas de p5LiveMedia, con esto estamos configurando todo el ambiente de p5.js
```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.1/p5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.1/addons/p5.sound.min.js"></script>
    <script type="text/javascript" src="https://p5livemedia.itp.io/simplepeer.min.js"></script>
    <script type="text/javascript" src="https://p5livemedia.itp.io/socket.io.js"></script>
    <script type="text/javascript" src="https://p5livemedia.itp.io/p5livemedia.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />

  </head>
  <body>
    <main>
    </main>
    <script src="sketch.js"></script>
  </body>
</html>
```
Paso 2: declarar las variables globales
```js
// Variables para videoconferencia
let myVideo; //guarda nuestro audio y video
let remoteVideo; // guarda el stream del video del otro usuario conectado
let p5lmVideo; //esta es la instancia que se encargda de la conexion de video/audio, es el capture

// Variables para tablero colaborativo
let p5lmData; // Esta es la instancia que comuncia los datos, es DATA
let drawingData = []; // el arreglo que guarda los trazos locales que hemos hecho
let remoteDrawings = []; // este guarda los trazos remotos

```
Paso 3: Hacemos el setup, configuramos todo

```js
function setup() {
  // Creamos un canvas que ocupará toda la ventana
  createCanvas(windowWidth, windowHeight);

  // Definimos constraints para capturar audio y video
  let constraints = { audio: true, video: true };

  // Sección de videoconferencia: ubicamos el video en la esquina superior izquierda
  myVideo = createCapture(constraints, function(stream) {
    // Se crea una instancia de p5LiveMedia para el stream de CAPTURE (video + audio)
    p5lmVideo = new p5LiveMedia(this, "CAPTURE", stream, "collabStudioRoom");
    // Se configura el callback para recibir streams remotos
    p5lmVideo.on('stream', gotRemoteVideo);
  });
  
  // Ajustamos el tamaño y posición del video local
  myVideo.size(320, 240);
  myVideo.position(20, 20);

  // Sección de tablero colaborativo:
  // Se crea una conexión de datos para enviar trazos
  p5lmData = new p5LiveMedia(this, "DATA", null, "collabStudioRoom");
  // Configuramos el callback para recibir datos de dibujo remotos
  p5lmData.on('data', gotDrawingData);
  
}

```

Paso 4: Configuramos el draw
```js
function draw() {
  // Fondo blanco para el tablero
  background(255);

  // Dibujar instrucciones en el tablero
  fill(0);
  textSize(16);
  text("Tablero Colaborativo - Dibuja con el mouse/táctil", 20, 300);

  // Dibujar trazos locales, recorre el arreglo local
  for (let d of drawingData) {
    stroke(d.color);
    strokeWeight(d.weight);
    line(d.x1, d.y1, d.x2, d.y2);
  }
  
  // Dibujar trazos remotos recibidos, recorre el arreglo remoto
  for (let d of remoteDrawings) {
    stroke(d.color);
    strokeWeight(d.weight);
    line(d.x1, d.y1, d.x2, d.y2);
  }
  
  // Si se ha recibido video remoto, se dibuja en la esquina superior derecha
  if (remoteVideo) {
    image(remoteVideo, width - 340, 20, 320, 240);
  }
}
```
Paso 5: Funcion mouseDragged() esta funcion se activa cuando empezamos a dibujar, guarda el trazo local, le da un color rojo, un grosor de 4 y lo envia en formato JSON

```js
function mouseDragged() {
  // Guardamos el trazo local
  let newStroke = {
    x1: pmouseX,
    y1: pmouseY,
    x2: mouseX,
    y2: mouseY,
    color: "#ff0000",    // Color rojo para trazos locales
    weight: 4
  };
  drawingData.push(newStroke);
  
  // Enviar el trazo en formato JSON a los demás usuarios
  p5lmData.send(JSON.stringify(newStroke));
}
```
Paso 6: Poner el callback del video y datos remoto, esta se ejecuta cunado se recibe el stream externo

```js
function gotRemoteVideo(stream, id) {
  // Se guarda el stream del video remoto
  remoteVideo = stream;
}

function gotDrawingData(data, id) {
  // Parseamos el JSON recibido y lo agregamos a los trazos remotos
  let d = JSON.parse(data);
  remoteDrawings.push(d);
}
// Ajustar el canvas al tamaño de la ventana en caso de redimensionar
function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
- Adiciona el código y enlaces necesarios para replicar la aplicación propuesta.

Codigo completo: 

```js
// Variables para videoconferencia
let myVideo; //guarda nuestro audio y video
let remoteVideo; // guarda el stream del video del otro usuario conectado
let p5lmVideo; //esta es la instancia que se encargda de la conexion de video/audio, es el capture

// Variables para tablero colaborativo
let p5lmData; // Esta es la instancia que comuncia los datos, es DATA
let drawingData = []; // el arreglo que guarda los trazos locales que hemos hecho
let remoteDrawings = []; // este guarda los trazos remotos
function setup() {
  // Creamos un canvas que ocupará toda la ventana
  createCanvas(windowWidth, windowHeight);

  // Definimos constraints para capturar audio y video
  let constraints = { audio: true, video: true };

  // Sección de videoconferencia: ubicamos el video en la esquina superior izquierda
  myVideo = createCapture(constraints, function(stream) {
    // Se crea una instancia de p5LiveMedia para el stream de CAPTURE (video + audio)
    p5lmVideo = new p5LiveMedia(this, "CAPTURE", stream, "collabStudioRoom");
    // Se configura el callback para recibir streams remotos
    p5lmVideo.on('stream', gotRemoteVideo);
  });
  
  // Ajustamos el tamaño y posición del video local
  myVideo.size(320, 240);
  myVideo.position(20, 20);

  // Sección de tablero colaborativo:
  // Se crea una conexión de datos para enviar trazos
  p5lmData = new p5LiveMedia(this, "DATA", null, "collabStudioRoom");
  // Configuramos el callback para recibir datos de dibujo remotos
  p5lmData.on('data', gotDrawingData);
  
}
function draw() {
  // Fondo blanco para el tablero
  background(255);

  // Dibujar instrucciones en el tablero
  fill(0);
  textSize(16);
  text("Tablero Colaborativo - Dibuja con el mouse/táctil", 20, 300);

  // Dibujar trazos locales, recorre el arreglo local
  for (let d of drawingData) {
    stroke(d.color);
    strokeWeight(d.weight);
    line(d.x1, d.y1, d.x2, d.y2);
  }
  
  // Dibujar trazos remotos recibidos, recorre el arreglo remoto
  for (let d of remoteDrawings) {
    stroke(d.color);
    strokeWeight(d.weight);
    line(d.x1, d.y1, d.x2, d.y2);
  }
  
  // Si se ha recibido video remoto, se dibuja en la esquina superior derecha
  if (remoteVideo) {
    image(remoteVideo, width - 340, 20, 320, 240);
  }
}
function mouseDragged() {
  // Guardamos el trazo local
  let newStroke = {
    x1: pmouseX,
    y1: pmouseY,
    x2: mouseX,
    y2: mouseY,
    color: "#ff0000",    // Color rojo para trazos locales
    weight: 4
  };
  drawingData.push(newStroke);
  
  // Enviar el trazo en formato JSON a los demás usuarios
  p5lmData.send(JSON.stringify(newStroke));
}
function gotRemoteVideo(stream, id) {
  // Se guarda el stream del video remoto
  remoteVideo = stream;
}

function gotDrawingData(data, id) {
  // Parseamos el JSON recibido y lo agregamos a los trazos remotos
  let d = JSON.parse(data);
  remoteDrawings.push(d);
}
// Ajustar el canvas al tamaño de la ventana en caso de redimensionar
function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

Link al archivo para editar de p5.js: https://editor.p5js.org/luciana.gp0531/sketches/Fpv6wn8St

Link al fullscreen: https://editor.p5js.org/luciana.gp0531/full/Fpv6wn8St
