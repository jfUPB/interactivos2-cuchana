#### Actividad 2:

- ¿Qué es p5LiveMedia?
  Es una biblioteca diseñada para p5.js que permite compartir en tiempo real video, audio, datos y el canva a través de el WebRTC, usa peer-to-peer, esto hace que los datos viajes directamente entre los navegadores sin necesidad de usar un server como intermediario.
  
- ¿Qué posibilidades ofrece p5LiveMedia?
  Con esta biblioteca podemos compartir video en vivo con nuestra cámara, enviar y recibir audio que capturamos desde el microfono, compartir el canva (tipo transmitirlo) para que lo vean en tiempo real, compartir datos en formato de texto entre usuarios.
  Hay 3 tipos de capturas, capture para audio y video, canvas y data.

- Replica varios ejemplos de p5LiveMedia que permitan entender sus posibilidades. Trata de seleccionar ejemplos para entender cómo se comparte audio, video, datos y el canvas.

- Compartir canva: Aqui creamos un canva y con p5LiveMedia lo compartimos con el otro cliente, cada cliente tiene su canva
  individual y lo podemos ver en nuestra pantalla
  
```js
let otherCanvas;

function setup() {
  // Creamos el canvas
  let myCanvas = createCanvas(400, 400);
  
  // Instanciamos p5LiveMedia para compartir el canvas
  let p5lm = new p5LiveMedia(this, "CANVAS", myCanvas, "salaCanvasEjemplo");
  p5lm.on('stream', gotStream);
}

function draw() {
  background(220);
  fill(255, 0, 0); // la tipica bolita roja
  ellipse(mouseX, mouseY, 100, 100);
}

function gotStream(stream) {
  // Recibimos el stream del canvas remoto
  otherCanvas = stream;
}
```

- Compartir canva y audio: Este ejemplo combina lo que hicimos anteriormente pero tambien usa el audioo del mic.
```js
  let myAudio, myCanvas, otherVideo;

function setup() {
  myCanvas = createCanvas(400, 400);

  // Se solicita solo audio en los constraints
  let constraints = { audio: true };
  myAudio = createCapture(constraints, function(stream) {
    // Capturamos el canvas como video a 15 fps
    let canvasStream = myCanvas.elt.captureStream(15);
    
    // Extraemos la pista de audio del stream capturado
    let audioTracks = stream.getAudioTracks();
    if (audioTracks.length > 0) {
      canvasStream.addTrack(audioTracks[0]);
    }
    
    // Compartimos el stream combinado (canvas + audio)
    let p5lm = new p5LiveMedia(this, "CAPTURE", canvasStream, "salaCanvasAudioEjemplo");
    p5lm.on('stream', gotStream);
  });

  myAudio.elt.muted = true;
  myAudio.hide(); // Oculta el elemento de video de la captura de audio
}

function draw() {
  background(220);
  fill(255, 0, 0);
  ellipse(mouseX, mouseY, 100, 100);
}

function gotStream(stream) {
  otherVideo = stream;
}
```
- Documenta en la bitácora tus hallazgos y las consideraciones que debes tener en cuenta para implementar p5LiveMedia en tu aplicación.

Descubri lo facil que es usar esta herramienta y usar funciones propias de p5.js para hacer el mismo stream, es muy flexibke porque nos permite compartir muchas entradas, el uso de los eventos (stream, data, connect y disconnect) permite tener toda ka actualizacion en tiempo real
muy conrolada, tambien es importante destacar que podemos hacer lo mismo de la unidad pasada pero sin usar server intermedios.
Algo que me parece super importante tener en cuenta es por nada del mundo olvidar inlcuir la biblioteca en el index, tambien evitar que podamos escuchar nuestra propia entrada de audio, 
