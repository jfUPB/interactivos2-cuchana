var tileCountX = 50;
var tileCountY = 50;

var hueValues = [];
var saturationValues = [];
var brightnessValues = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();

  for (var i = 0; i < tileCountX; i++) {
    hueValues[i] = random(360);
    saturationValues[i] = random(100);
    brightnessValues[i] = random(100);
  }
}

function draw() {
  background(0, 0, 100);

  var mX = constrain(mouseX, 0, width);
  var mY = constrain(mouseY, 0, height);

  var counter = 0;
  var currentTileCountX = int(map(mX, 0, width, 1, tileCountX));
  var currentTileCountY = int(map(mY, 0, height, 1, tileCountY));
  var tileWidth = width / currentTileCountX;
  var tileHeight = height / currentTileCountY;

  for (var gridY = 0; gridY < tileCountY; gridY++) {
    for (var gridX = 0; gridX < tileCountX; gridX++) {
      var posX = tileWidth * gridX;
      var posY = tileHeight * gridY;
      var index = counter % currentTileCountX;

      // Cambio MUY lento en los valores de color
      hueValues[index] = (hueValues[index] + sin(frameCount * 0.0002)) % 360;
      saturationValues[index] = constrain(saturationValues[index] + cos(frameCount * 0.0001) * 0.2, 40, 100);
      brightnessValues[index] = constrain(brightnessValues[index] + sin(frameCount * 0.0001) * 0.2, 50, 100);

      fill(hueValues[index], saturationValues[index], brightnessValues[index]);
      rect(posX, posY, tileWidth, tileHeight);
      counter++;
    }
  }
}
