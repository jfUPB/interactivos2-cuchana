#### Actividad #4 

**Ejemplo 1:** 

Kunst 1 by KodeSkolen:

https://openprocessing.org/sketch/906922

- Descripción del código: El codigo original es super sencillo tenemos un canva, con un fondo gris, y en draw tenemos que el trazo del mouse dibuje elipses blancas.
```js
    function setup() {
  	createCanvas(windowWidth, windowHeight);
  	background(100, 100, 100);
  }
  
  function draw() {
  	ellipse(mouseX, mouseY, 100, 100);
  	fill(255, 255, 255);
  	
  }	
```

Modificación del código: Quise cambiarle la forma, cambiar la elipse por un corazon y dar la opcion de escoger un color, con las teclas R(rojo), G (verde) B (azul) Y P (rosado), como implemente cambio de color decidi mejor cambiar el trazo a que siga la posicion del mouse cuando haga click

```js
let colors = [
  { r: 255, g: 0, b: 0 },     // Rojo
  { r: 0, g: 255, b: 0 },     // Verde
  { r: 0, g: 0, b: 255 },     // Azul
  { r: 255, g: 255, b: 0 },   // Amarillo
  { r: 255, g: 105, b: 180 }, // Rosa
];

let currentColorIndex = 0; // color actual

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(100, 100, 100);
}

function draw() {
  // Solo dibuja corazones cuando el mouse está presionado
  if (mouseIsPressed) {
    fill(colors[currentColorIndex].r, colors[currentColorIndex].g, colors[currentColorIndex].b);
    stroke(0);       // Contorno negro
    drawHeart(mouseX, mouseY, 50);  // Tamaño del corazón
  }
}

// Función para dibujar un corazón en una posición específica, la recicle de un ejercicio de sfi1 
function drawHeart(x, y, size) {
  beginShape();
  vertex(x, y);
  bezierVertex(x - size / 2, y - size / 2, x - size, y + size / 3, x, y + size);
  bezierVertex(x + size, y + size / 3, x + size / 2, y - size / 2, x, y);
  endShape(CLOSE);
}

function keyPressed() {
  // Cambiar el color con las teclas R, G, B, Y, P
  if (key === 'R' || key === 'r') currentColorIndex = 0; // Rojo
  if (key === 'G' || key === 'g') currentColorIndex = 1; // Verde
  if (key === 'B' || key === 'b') currentColorIndex = 2; // Azul
  if (key === 'Y' || key === 'y') currentColorIndex = 3; // Amarillo
  if (key === 'P' || key === 'p') currentColorIndex = 4; // Rosa
}
```
![image](https://github.com/user-attachments/assets/20d0b9ed-6582-4142-9ff7-b6e6db7d5964)


**Ejemplo 2:**
Genuary 10: You can only use TAU in your code

Descripción del código: Este código genera una animación en la que formas geométricas (basadas en polígonos) se dibujan utilizando ruido Simplex para crear movimientos y cambios de forma en el tiempo. Los colores de las formas también cambian dinámicamente, y se muestra el texto "TAU" al final del lienzo.

```js
let simplex
let colors=["#c69322","#c0bd9b","#a08b8d","#005e84","#42a5e4","#4ad3c8","#02c287"]
let single, indent,ttl, tt, ttp, ttpp, ttppp, tttl, center, ttt, inc, nearBottom, incp, bgc


function preload(){
font= loadFont('FamiljenGrotesk-VariableFont_wght.ttf')
	bgc= '#f4f1de'
}

function setup() {
	single= TAU/TAU //1
	let t= TAU//6.28
	indent= t+t+t+single
	ttl= TAU*TAU-TAU//33
	tt= TAU*TAU  //39
	ttp= ttl+ttl //66
	ttpp= ttl+ttl+ttl //99.58
	ttppp=ttl+ttl+ttl+ttl
	tttl= TAU*TAU*TAU-TAU//241
	center= tttl-tt-single-single//center
	ttt= TAU * TAU*TAU //248
	inc=ttl/ttt //0.133
	incp= inc+inc
	nearBottom=ttt+ttpp+tt
	let cs= center+center
  createCanvas(cs, cs); 
	simplex= new openSimplexNoise(Date.now())
	background(bgc)
}

function draw(){
	background(bgc)
	noStroke()
	for(let r=ttppp; r>TAU; r-=single){
		fill(colorMixer(r, colors))
	beginShape()
	for(let a=0; a<TAU; a+=inc){
		let roff= simplex.noise4D(cos(a), sin(a), r*incp*incp, frameCount*inc*inc)*(TAU+TAU+single)
    vertex(center+cos(a)*(r+roff), center+sin(a)*(r+roff))
		
	}
	endShape(CLOSE)
	}
	
	noStroke()
	textFont(font)
	 fill(ttpp)
	stroke(ttpp)
  text('TAU', indent, nearBottom)  
	
}


function colorMixer(r, colorArray, alpha) {
	let timer= frameCount*inc*inc*incp
	let c = noise(r*incp*incp+timer) * colorArray.length
	let cc = floor(c)
	let ccc = floor(c + single) % colorArray.length
	let colora = colorArray[cc]
	let colorb = colorArray[ccc]
	let mix = fract(c)
	let coloring = color(spectral.mix(colora, colorb, mix))
	return coloring
}
```

Modificación del código: Cambie los colores y la forma que genera, en vez de un circulo hace un rombo, con una funcion de un cuadrado rotado.

cambie toda la función original del circulo, desde el for a < 4 hasta el calculo de posicion con cos y sin.

```js
let angle = a * TWO_PI / 4;  // Cada ángulo de 90 grados (TWO_PI / 4)
      let roff = noise(cos(angle) * r * incp * incp, sin(angle) * r * incp * incp, frameCount * inc * inc) * (TAU + TAU + single);
      
      // Defino las coordenadas de los vértices de un cuadrado rotado
      let x = center + cos(angle) * (r + roff); // Posición X
      let y = center + sin(angle) * (r + roff); // Posición Y
      vertex(x, y); // Dibuja el vértice
```

```js

let simplex
let colors=["#7fc8f8","#DD88D4","#7BDAA3","#AEDD77","#E44242","#4ad3c8","#02c287"]
let single, indent,ttl, tt, ttp, ttpp, ttppp, tttl, center, ttt, inc, nearBottom, incp, bgc


function preload(){
font= loadFont('FamiljenGrotesk-VariableFont_wght.ttf')
	bgc= '#f4f1de'
}

function setup() {
	single= TAU/TAU //1
	let t= TAU//6.28
	indent= t+t+t+single
	ttl= TAU*TAU-TAU//33
	tt= TAU*TAU  //39
	ttp= ttl+ttl //66
	ttpp= ttl+ttl+ttl //99.58
	ttppp=ttl+ttl+ttl+ttl
	tttl= TAU*TAU*TAU-TAU//241
	center= tttl-tt-single-single//center
	ttt= TAU * TAU*TAU //248
	inc=ttl/ttt //0.133
	incp= inc+inc
	nearBottom=ttt+ttpp+tt
	let cs= center+center
  createCanvas(cs, cs); 
	simplex= new openSimplexNoise(Date.now())
	background(bgc)
}

function draw(){
	background(bgc)
	noStroke()
	for(let r=ttppp; r>TAU; r-=single){
		fill(colorMixer(r, colors))
	beginShape()
	for(let a = 0; a < 4; a++){
		    // Cambié el cálculo de la posición con cos() y sin() a una lógica de cuadrado
      let angle = a * TWO_PI / 4;  // Cada ángulo de 90 grados (TWO_PI / 4)
      let roff = noise(cos(angle) * r * incp * incp, sin(angle) * r * incp * incp, frameCount * inc * inc) * (TAU + TAU + single);
      
      // Defino las coordenadas de los vértices de un cuadrado rotado
      let x = center + cos(angle) * (r + roff); // Posición X
      let y = center + sin(angle) * (r + roff); // Posición Y
      vertex(x, y); // Dibuja el vértice
		
	}
	endShape(CLOSE)
	}
	
	noStroke()
	textFont(font)
	 fill(ttpp)
	stroke(ttpp)
  text('TAU', indent, nearBottom)  
	
}


function colorMixer(r, colorArray, alpha) {
	let timer= frameCount*inc*inc*incp
	let c = noise(r*incp*incp+timer) * colorArray.length
	let cc = floor(c)
	let ccc = floor(c + single) % colorArray.length
	let colora = colorArray[cc]
	let colorb = colorArray[ccc]
	let mix = fract(c)
	let coloring = color(spectral.mix(colora, colorb, mix))
	return coloring
}

```

Reflexión: Este ejercicio me sirvio mucho para repasar las bases de p5.js, tambien para aprender nuevas bibliotecas como el noise, el cargar fuentes, etc
