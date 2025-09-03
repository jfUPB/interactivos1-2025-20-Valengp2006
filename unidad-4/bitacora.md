# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/P_1_1_2_01)

Código a modificar:

``` js
'use strict';

var segmentCount = 360;
var radius = 300;

function setup() {
  createCanvas(800, 800);
  noStroke();
}

function draw() {
  colorMode(HSB, 360, width, height);
  background(360, 0, height);

  var angleStep = 360 / segmentCount;

  beginShape(TRIANGLE_FAN);
  vertex(width / 2, height / 2);

  for (var angle = 0; angle <= 360; angle += angleStep) {
    var vx = width / 2 + cos(radians(angle)) * radius;
    var vy = height / 2 + sin(radians(angle)) * radius;
    vertex(vx, vy);
    fill(angle, mouseX, mouseY);
  }

  endShape();
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');

  switch (key) {
  case '1':
    segmentCount = 360;
    break;
  case '2':
    segmentCount = 45;
    break;
  case '3':
    segmentCount = 24;
    break;
  case '4':
    segmentCount = 12;
    break;
  case '5':
    segmentCount = 6;
    break;
  }
}

```

[Enlace a la aplicación modificada](https://editor.p5js.org/Valengp2006/sketches/MWujJvEw_)

Código modificado:

``` js
// === VARIABLES DEL DIBUJO ===
var segmentCount = 360; // Número inicial de segmentos
var radius = 300;       // Radio del dibujo

// === VARIABLES DE COLOR ===
let saturationValue = 0; // Controlado por el acelerómetro X del Micro:bit
let brightnessValue = 0; // Controlado por el acelerómetro Y del Micro:bit

// === VARIABLES DE CONEXIÓN MICRO:BIT ===
let port; // Objeto para el puerto serial
let connectBtn; // Botón para conectar/desconectar
let microBitConnected = false; // Estado de la conexión
let aWasPressed = false; // Para el 'debouncing' del Botón A
let bWasPressed = false; // Para el 'debouncing' del Botón B

function setup() {
    // Crea un lienzo dinámico que ocupa la mayoría del espacio de la ventana
    createCanvas(800 , 800);
    noStroke(); // Sin bordes para las formas

    // Inicializa los valores de saturación y brillo al centro
    saturationValue = width / 2;
    brightnessValue = height / 2;

    // Configuración del puerto serial
    port = createSerial();

    // Crea el botón de conexión y le asigna el evento de ratón
    connectBtn = createButton("Conectar Micro:bit");
    connectBtn.mousePressed(connectBtnClick);
    // Asigna el botón al div con ID "controls" en el HTML
    connectBtn.parent('controls');

    // Estilos básicos para el botón
    connectBtn.style('padding', '10px 20px');
    connectBtn.style('font-size', '16px');
    connectBtn.style('border-radius', '5px');
    connectBtn.style('background-color', '#4CAF50');
    connectBtn.style('color', 'white');
    connectBtn.style('border', 'none');
    connectBtn.style('cursor', 'pointer');
    connectBtn.style('margin', '5px');
}

function draw() {
    // Maneja la conexión serial en cada fotograma
    handleSerialConnection();
  
    colorMode(HSB, 360, width, height);
    background(360, 0, height);

    // Calcula el paso del ángulo para los segmentos
    var angleStep = 360 / segmentCount;

    // Inicia el dibujo de las formas (TRIANGLE_FAN dibuja triángulos desde un punto central)
    beginShape(TRIANGLE_FAN);
    // El vértice central del dibujo
    vertex(width / 2, height / 2);

    // Bucle para dibujar cada segmento
    for (var angle = 0; angle <= 360; angle += angleStep) {
        // Calcula las coordenadas del vértice en el borde del círculo
        var vx = width / 2 + cos(radians(angle)) * radius;
        var vy = height / 2 + sin(radians(angle)) * radius;
        vertex(vx, vy);

        // Rellena el segmento con color HSB
        // El tono (hue) cambia con el ángulo, la saturación y el brillo son controlados por Micro:bit
        fill(angle, saturationValue, brightnessValue);
    }
    endShape(); // Termina el dibujo de la forma
}

// === FUNCIONES DE CONEXIÓN Y PROCESAMIENTO MICRO:BIT ===

function handleSerialConnection() {
    // Si el puerto no está abierto, actualiza el texto del botón y el estado de conexión
    if (!port.opened()) {
        connectBtn.html("Conectar Micro:bit");
        microBitConnected = false;
    } else {
        // Si el puerto está abierto, actualiza el texto del botón y el estado
        connectBtn.html("Desconectar");
        microBitConnected = true;

        // Lee datos del puerto serial hasta que encuentra un salto de línea
        let dataString = port.readUntil("\n");
        if (dataString) {
            processMicroBitData(dataString.trim()); // Procesa los datos recibidos
        }
    }
}

function processMicroBitData(data) {
    let values = data.split(","); // Divide la cadena de datos por comas
    // El formato esperado es: accelX, accelY, a_pressed, b_pressed
    if (values.length === 4) {
        let accelX = parseInt(values[0]); // Valor del acelerómetro en X
        let accelY = parseInt(values[1]); // Valor del acelerómetro en Y
        let aPressed = (values[2] === "True"); // Estado del Botón A (True/False)
        let bPressed = (values[3] === "True"); // Estado del Botón B (True/False)

        // === ACELERÓMETRO X -> SATURACIÓN ===
        // Mapea el valor del acelerómetro X (-1024 a 1024) al rango de saturación (0 a 'width')
        saturationValue = map(accelX, -1024, 1024, 0, width);
        // Asegura que la saturación esté dentro de los límites
        saturationValue = constrain(saturationValue, 0, width);

        // === ACELERÓMETRO Y -> BRILLO ===
        // Mapea el valor del acelerómetro Y (-1024 a 1024) al rango de brillo (0 a 'height')
        brightnessValue = map(accelY, -1024, 1024, 0, height);
        // Asegura que el brillo esté dentro de los límites
        brightnessValue = constrain(brightnessValue, 0, height);
        
        // === BOTÓN B -> CAMBIAR A segmentCount = 6 (equivalente a tecla '5') ===
        // Implementa un 'debouncing' para que el botón B solo cambie una vez por pulsación
        if (bPressed && !bWasPressed) {
            segmentCount = 6; // Establece segmentCount a 6
            port.write('r'); // Envía una señal al Micro:bit para indicar que se procesó el botón
        }
        bWasPressed = bPressed; // Actualiza el estado del botón B

        // === BOTÓN A -> CAMBIAR A segmentCount = 360 (equivalente a tecla '1') ===
        // Implementa un 'debouncing' para que el botón A solo actúe una vez por pulsación
        if (aPressed && !aWasPressed) {
            segmentCount = 360; // Establece segmentCount a 360 (como si se presionara '1')
            // La funcionalidad de guardar imagen se ha movido solo a la tecla 's' del teclado.
            port.write('r'); // Envía una señal al Micro:bit para indicar que se procesó el botón
        }
        aWasPressed = aPressed; // Actualiza el estado del botón A
    }
}

// === FUNCIÓN DEL BOTÓN DE CONEXIÓN ===
function connectBtnClick() {
    // Si el puerto no está abierto, ábrelo
    if (!port.opened()) {
        // "MicroPython" es el nombre del dispositivo, 115200 es la velocidad en baudios
        port.open("MicroPython", 115200);
    } else {
        // Si el puerto está abierto, ciérralo
        port.close();
    }
}

// === MANEJO DE TECLAS (MANTIENE LA FUNCIONALIDAD ORIGINAL PARA 2, 3, 4 y 's') ===
function keyPressed() {
    // Guarda el lienzo ÚNICAMENTE si se presiona 's' o 'S'
    if (key == 's' || key == 'S') 
        saveCanvas(gd.timestamp(), 'png');

    // Cambia el número de segmentos según la tecla presionada
    switch (key) {
        // Los casos '1' y '5' ahora son manejados principalmente por los botones del Micro:bit,
        // pero la funcionalidad de teclado se mantiene intacta aquí.
        case '1':
            segmentCount = 360;
            break;
        case '2':
            segmentCount = 45;
            break;
        case '3':
            segmentCount = 24;
            break;
        case '4':
            segmentCount = 12;
            break;
        case '5':
            segmentCount = 6;
            break;
    }
}
```

## Video

[Video demostratativo](https://youtu.be/nIx9nVPlox4?si=Wn76gzjzWohzKwDI)









