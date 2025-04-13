#### Actividad #11: 

Crea un programa en p5.js que genere texto aleatorio a partir de un conjunto de caracteres o palabras predefinidas. Experimenta con diferentes fuentes, tamaños y estilos de texto. Puedes intentar generar poemas o frases aleatorias.

Primero creamos un arreglo con las palabras pre-definidas, entonces como queremos una frase de 3 palabras 
entonces necesitamos 3 arreglos.
Almacenamos la fuente, el tamaño, color y la frase, todas estas variables serán aleatorias, solo 
cambian con cada click. Cargamos una fuente predeterminada.
El texto generado es parte1, parte2 y parte3, que cada una es un random a el respectivo arreeglo.

```js
let words = [
  ["Hola", "Buenas", "Oe", "Hablalo", "Ey"],
  [",que mas?", ",como vas?", ",como estas?", ",bien o no?", ",melo?"],
  ["la buena", "todo bien", "nospi", "las mejores", "hasta luego"]];

let fonts = [];
let selectedFont;
let fontSize;
let textColor;
let generatedText;

function preload() {
  fonts.push(loadFont('https://cdnjs.cloudflare.com/ajax/libs/topcoat/0.8.0/font/SourceCodePro-Bold.otf'));
  fonts.push(loadFont('https://cdnjs.cloudflare.com/ajax/libs/topcoat/0.8.0/font/SourceSansPro-Bold.otf'));
}

function setup() {
  createCanvas(600, 400);
  textAlign(CENTER, CENTER);
  generateText();
}

function draw() {
  background(240);
  fill(textColor);
  textFont(selectedFont);
  textSize(fontSize);
  text(generatedText, width / 2, height / 2);
}

function generateText() {
  let part1 = random(words[0]);
  let part2 = random(words[1]);
  let part3 = random(words[2]);

  generatedText = `${part1} ${part2} ${part3}.`;
  selectedFont = random(fonts);
  fontSize = random([24, 32, 40, 48, 56]);
  textColor = color(random(50, 200), random(50, 200), random(50, 200));
}

function mousePressed() {
  generateText();
}
```

![image](https://github.com/user-attachments/assets/c088643f-732a-4752-990f-9aa497ce9270)
