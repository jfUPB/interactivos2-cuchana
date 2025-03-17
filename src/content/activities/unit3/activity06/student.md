#### Actividad 6: 

Vas a construir una aplicación que le permita a un cliente capturar una imagen de su cámara o del sistema de archivos y enviarla a otro cliente remoto.

Entrega: muestra el código de la aplicación: servidor y clientes. 

**Codigo sketch.js Desktop:**

```js
// desktop

let socket;
let capture;
let captureButton;
let sendButton;
let fileInput;
let imgCanvas;

function setup() {
    createCanvas(400, 400);
    background(220);

    let socketUrl = 'http://localhost:3000';
    socket = io(socketUrl);

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    // Inicializar la cámara
    capture = createCapture(VIDEO);
    capture.size(400, 300);
    capture.hide(); // Ocultar el video en vivo

    // Botón para tomar foto
    captureButton = createButton('Tomar Foto');
    captureButton.position(10, height + 10);
    captureButton.mousePressed(takePhoto);

    // Botón para enviar la foto
    sendButton = createButton('Enviar Foto');
    sendButton.position(110, height + 10);
    sendButton.mousePressed(sendPhoto);
    sendButton.hide(); // Se mostrará después de tomar una foto

    // Input para subir imágenes
    fileInput = createFileInput(handleFile);
    fileInput.position(250, height + 10);
}

// Tomar una foto con la cámara
function takePhoto() {
    imgCanvas = capture.get(); // Capturar imagen actual del video
    sendButton.show(); // Mostrar botón de enviar
}

// Manejar una imagen subida desde el sistema de archivos
function handleFile(file) {
    if (file.type === 'image') {
        console.log('Imagen cargada desde archivos');
        imgCanvas = loadImage(file.data, () => {
            sendPhoto(); // Enviar la imagen automáticamente
        });
    }
}

// Enviar la imagen al servidor
function sendPhoto() {
    if (imgCanvas) {
        let imgData = imgCanvas.canvas.toDataURL(); // Convertir a Base64
        console.log('Enviando imagen...');
        socket.emit('image', imgData);
        sendButton.hide(); // Ocultar botón de enviar después de enviarla
    }
}

function draw() {
    background(220);
    image(capture, 0, 0, 400, 300); // Mostrar el video en vivo

    if (imgCanvas) {
        image(imgCanvas, 50, 320, 100, 75); // Previsualizar la imagen tomada o cargada
    }
}
```


**Código sketch.js Mobile:**
```js
// mobile

let socket;
let imgElement;

function setup() {
    createCanvas(400, 400);
    background(220);

    let socketUrl = 'http://localhost:3000';
    socket = io(socketUrl);

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    // Recibir imagen desde el servidor
    socket.on('image', (data) => {
        console.log('Imagen recibida');

        if (imgElement) {
            imgElement.remove(); // Eliminar imagen anterior
        }

        imgElement = createImg(data, 'Foto recibida');
        imgElement.hide(); // Ocultar HTML

        // Asegurar que se redibuja correctamente
        setTimeout(() => {
            redraw(); // Forzar redibujado después de recibir la imagen
        }, 100);
    });

    noLoop(); // Evita que draw() se ejecute en bucle
}

function draw() {
    background(220);
    if (imgElement) {
        image(imgElement, 50, 50, 300, 300); // Dibujar la imagen en el canvas
    }
}
```


Explica claramente:

¿Cómo se comunican los clientes con el servidor?
- Desktop y mobile se conectan a traves de el Socket.IO, desktop envia las imagenes, el server las recibe y las envia a mobile y la renderiza.

  
¿Cómo se comunican los clientes entre sí?
- Por medio del server

¿Qué tipo de mensajes se envían?
- Image, que contiene la imagen cargada o tomada.

¿Qué tipo de datos se envían?
- png

¿Qué tipo de eventos se generan?
- Connect: indica que uno de los clientes se conectó
- Disconnect: este por el contrario nos dice que cliente se desconectó
- image: envia una imagen png y despues es quien lo reenvia a otros clientes

¿Cómo es el flujo de datos entre los clientes y el servidor?
1. El cliente Desktop captura o carga una imagen
2. Envia la imagen al servidor
3. El servidor recibe la imagen y con io.emit la reenvía a todos los clientes.
4. El cliente Mobile recibe la imagen y la proyecta en el canvas

¿Cómo es el flujo de datos entre los clientes?
- los clientes no se comunican directamente
- Desktop siempre envia imagenes al servidor
- Mobile las recibe del server
- El server es el puente que envia las imagenes
  


