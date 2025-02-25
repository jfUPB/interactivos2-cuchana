#### Actividad #13

Utilizando la biblioteca p5.sound (u otra que quieras probar), experimenta con la generación de sonidos básicos. Intenta crear diferentes tipos de ondas sonoras (senoidal, triangular, cuadrada) y modificar sus parámetros (frecuencia, amplitud) para generar diferentes tonos y timbres.

Use p5.Oscillator, esta clase me la proporcionó ChatGPT (si funciona profe, no se la inventó),hay que definir el tipo de onda, debemos definir qué tipo de onda queremos usar, su frecuencia y amplitud.

El mouse define la frecuencia en X, de 100 a 1000 Hz, y la amplitud en Y de 1 a 0, invirtiendo el valor para que arriba sea más fuerte y abajo más bajo. El tipo de onda se cambia con los números de 1 a 4.

```js
let osc;
let waveType = 'sine'; // iniciamos con esta onda

function setup() {
  createCanvas(400, 200);
  osc = new p5.Oscillator(); // crea el oscilador
  osc.setType(waveType); // con esto cambiamos el tipo de onda
  osc.freq(440); // frecuencia inicial
  osc.amp(0.5); // amplitud inicial
  osc.start(); // activa el sonido
}

function draw() {
  background(255,192,203);
  
  let freq = map(mouseX, 0, width, 100, 1000); // dirige X a frecuencia
  let amp = map(mouseY, 0, height, 1, 0); // este dirige Y a amplitud 
  
  // aqui ajustamos la frecuencia y la amplitud
  osc.freq(freq); 
  osc.amp(amp); 

  fill(255);
  textAlign(CENTER, CENTER);
  textSize(16);
  text("Presiona 1-4 para cambiar el tipo de onda", width / 2, 50);
  text(`Onda actual: ${waveType}`, width / 2, 100);
  text(`Frecuencia: ${nf(freq, 0, 2)} Hz`, width / 2, 130);
  text(`Amplitud: ${nf(amp, 0, 2)}`, width / 2, 160);
}

function keyPressed() {
  if (key === '1') waveType = 'sine';
  if (key === '2') waveType = 'triangle';
  if (key === '3') waveType = 'square';
  if (key === '4') waveType = 'sawtooth';
  
  osc.setType(waveType);
}
```
