# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/P_2_1_3_05)

Código a modificar:

``` js
'use strict';

var tileCountX = 10;
var tileCountY = 10;
var tileWidth;
var tileHeight;

var colorStep = 6;

var endSize = 0;
var stepSize = 30;

var actRandomSeed = 0;

function setup() {
  createCanvas(600, 600);
  noStroke();
  tileWidth = width / tileCountX;
  tileHeight = height / tileCountY;
}

function draw() {
  background(255);

  randomSeed(actRandomSeed);

  stepSize = min(mouseX, width) / 10;
  endSize = min(mouseY, height) / 10;

  for (var gridY = 0; gridY <= tileCountY; gridY++) {
    for (var gridX = 0; gridX <= tileCountX; gridX++) {

      var posX = tileWidth * gridX;
      var posY = tileHeight * gridY;

      // modules
      var heading = int(random(4));
      for (var i = 0; i < stepSize; i++) {
        var diameter = map(i, 0, stepSize, tileWidth, endSize);
        fill(255 - i * colorStep);
        switch (heading) {
        case 0: ellipse(posX + i, posY, diameter, diameter); break;
        case 1: ellipse(posX, posY + i, diameter, diameter); break;
        case 2: ellipse(posX - i, posY, diameter, diameter); break;
        case 3: ellipse(posX, posY - i, diameter, diameter); break;
        }
      }
    }
  }
}

function mousePressed() {
  actRandomSeed = random(100000);
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}

```

[Enlace a la aplicación modificada](URL)

Código modificado:

``` js

```

## Video

[Video demostratativo](URL)


