#### Actividad #12

Utilizando p5.js, carga una imagen y experimenta con la manipulación de sus píxeles para crear efectos visuales generativos. Puedes probar a cambiar el color, la posición o la transparencia de los píxeles basándote en su posición o en valores aleatorios.

Quise ponerle un filtro de desenfoque y alterar la saturación, para desenfocar use img.filter(BLUR, INTENSIDAD) y una funcion que se llama saturar, esta la hice con chatgpt que pasa de RGB a HSB para poder aplicar la saturacion, y cuando lo altera lo devuelve a RGB.

```js
let img;

function preload() {
  img = loadImage('nationalgeographic_1468962.jpg'); // aqui cargue la imagen 
}

function setup() {
  createCanvas(600, 400);
  img = saturar(img); // Aumentar saturación
  img.filter(BLUR, 10); // Aplicamos el desenfoque, le puse la intensidad en 10 para que se pueda ver el cambio aplicado
  image(img, 0, 0, width, height);
  noLoop(); //esto es para que la imagen no se regenere en cada update
}

// función para aumentar la saturación de la foto
function saturar(imgSection) {
  imgSection.loadPixels();
  
  for (let i = 0; i < imgSection.pixels.length; i += 4) {
    let r = imgSection.pixels[i];
    let g = imgSection.pixels[i + 1];
    let b = imgSection.pixels[i + 2];

    // Convertir RGB a HSB y modificar la saturación
    colorMode(HSB, 255);
    let c = color(r, g, b);
    let h = hue(c);
    let s = constrain(saturation(c) * 1.5, 0, 255); // Aumenta saturación
    let bValue = brightness(c);

    // Convertir de vuelta a RGB
    colorMode(RGB, 255);
    let newColor = color(h, s, bValue);
    
    imgSection.pixels[i] = red(newColor);
    imgSection.pixels[i + 1] = green(newColor);
    imgSection.pixels[i + 2] = blue(newColor);
  }
  
  imgSection.updatePixels();
  return imgSection;
}
```
