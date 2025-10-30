# Evidencias de la unidad 8

## Actividad 01 - 22/10/2025

### Tema musical

**“Main Theme – Interstelar” – Hans Zimmer**

La composición transmite la inmensidad del universo y la dualidad entre lo humano y lo cósmico. Esta experiencia interactiva busca recrear ese sentimiento de asombro y conexión emocional mediante una simulación inmersiva que combina sonido, luz y movimiento en tiempo real.

### Concepto general de la experiencia

La aplicación propone una **exploración interactiva del espacio exterior**, ambientada con el tema principal de *Interstelar*.
El usuario se convierte en el **piloto de una nave interestelar**, controlando su trayecto a través de un entorno 3D lleno de estrellas, nebulosas y planetas generados mediante **Three.js**, mientras interactúa con una **consola de vuelo táctil** creada en **p5.js** y un **micro:bit** que actúa como dispositivo físico complementario.

El objetivo es crear una experiencia **multiplataforma sincronizada** entre dispositivos, donde cada uno cumple un rol dentro del sistema interactivo:

- **Celular:** interfaz visual y táctil (panel de control).
- **Micro:bit:** control físico con botones y sensores.
- **Computador:** entorno inmersivo tridimensional y visualización de respuestas en tiempo real.

### Referentes visuales y conceptuales

1. [Video de Universo 360](https://www.youtube.com/watch?v=kMVV6YjaGM4)
2. [Viaje 360 por el Sistema Solar](https://www.youtube.com/watch?v=xdURfh5OPjQ)
3. [Película *Interestelar*](https://www.netflix.com/co/title/70305903)
4. Controlador de nave espacial:
<img width="626" height="403" alt="image" src="https://github.com/user-attachments/assets/40c8ed55-bc59-409c-9457-0979b202a8c2" />


### Concepto de interacción

#### Micro:bit – Control físico principal

| Elemento         | Función                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------- |
| **Botón A**      | Enciende o apaga los motores de la nave (activa/pausa la música y los efectos visuales). |
| **Botón B**      | Modifica la intensidad o tonalidad de la iluminación general.                            |
| **Shake**        | Reinicia la simulación a su estado inicial.                                              |
| **Acelerómetro** | Control de dirección: al inclinar el micro:bit, la nave gira o asciende en el espacio.   |

#### Celular – Consola de vuelo táctil (p5.js)

El panel fue diseñado en **p5.js** con inspiración en las consolas de vuelo espaciales vistas desde arriba, similar a la referencia visual mostrada.
Cada elemento del panel cumple una función específica dentro de la experiencia:

| Elemento                             | Función                                                                      |
| ------------------------------------ | ---------------------------------------------------------------------------- |
| **Palanca principal (derecha)**      | Control de velocidad de la nave (acelerar o desacelerar).                    |
| **Palancas secundarias (izquierda)** | Ajuste de rotación y orientación.                                            |
| **Deslizadores**                     | Controlan la intensidad de efectos visuales (nebulosas, brillo, partículas). |
| **Botón triangular rojo**            | Inicia la secuencia de salto interestelar (transición de escena).            |
| **Botones verdes**                   | Cambian el color del cielo o los efectos atmosféricos.                       |
| **Pantalla central**                 | Indica el estado del sistema (velocidad, energía, color activo).             |

El panel se comunica con el computador mediante **Socket.IO**, enviando y recibiendo datos en tiempo real para modificar los parámetros del entorno visual y la música.

#### Computador – Entorno inmersivo 3D (Three.js)

La visualización principal está desarrollada en **Three.js**, y representa un **viaje espacial en primera persona**.
El entorno incluye:

- **Simulación de estrellas y nebulosas dinámicas.**
- **Reactividad visual al audio:** el ritmo y volumen del tema de *Interstellar* afectan el movimiento de partículas y la iluminación.
- **Eventos interactivos:** al presionar el botón rojo o aumentar la velocidad, se ejecutan efectos visuales como distorsión o “salto cuántico”.
- **Sincronización total:** los comandos enviados desde el celular y el micro:bit modifican en tiempo real el entorno 3D.

### Flujo de comunicación del sistema

```text
┌─────────────┐          ┌──────────────┐          ┌─────────────┐
│  micro:bit  │──UART──▶│   Servidor   │◀──socket──│   Celular   │
│ (botones y  │          │ Node.js +    │──socket──▶│ (panel táctil)│
│ acelerómetro)│          │ Socket.IO    │          └─────────────┘
└──────┬──────┘          └──────┬───────┘
       │                        │
       ▼                        ▼
 ┌────────────────────────────────────┐
 │       Cliente de Escritorio        │
 │ (Three.js + p5.js visuales 360°)  │
 │      + música “Interstellar”      │
 └────────────────────────────────────┘
```

Cada dispositivo funciona como un módulo dentro del ecosistema:

- **Micro:bit:** entrada física (hardware).
- **Celular:** interfaz táctil (UI).
- **Computador:** procesamiento visual (render 3D).
- **Servidor Node.js:** puente de comunicación entre los tres.

### Diseño visual y experiencia

1. **Panel táctil móvil:**
   Creado con p5.js, su diseño combina botones, sliders y palancas en vista cenital. Cada elemento reacciona visualmente al tacto mediante animaciones y luces suaves, reforzando la sensación de control real.

2. **Micro:bit:**
   Se sostiene con la mano no dominante y permite controlar la dirección de la nave. Su vibración o respuesta lumínica podría indicar acciones clave (inicio, pausa, salto interestelar).

3. **Pantalla del computador:**
   Muestra un entorno espacial inmersivo en Three.js, donde la música guía el movimiento de las partículas y el brillo del entorno. El usuario percibe cómo cada acción física o táctil altera la composición visual, creando una **sincronía sensorial entre luz, sonido y control**.

### Conclusión

Esta experiencia combina **interacción tangible y digital**, explorando cómo diferentes medios (hardware, touch y visual 3D) pueden integrarse en una narrativa emocional.
A través del lenguaje visual y sonoro de *Interstellar*, el usuario experimenta el control de una nave espacial en un viaje simbólico que une **tecnología, música y emoción** en tiempo real.

# Actividad 02 - 24/10/2025

### `Código desktop/index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Simulación 3D Controlada por Micro:bit</title>

  <!-- Librerías -->
  <script src="https://cdn.jsdelivr.net/npm/three@0.152.0/build/three.min.js"></script>
  <script defer src="sketch.js"></script>

  <style>
    body { margin: 0; overflow: hidden; background: #000; }
    canvas { display: block; }
    button {
      position: absolute;
      top: 20px;
      left: 20px;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      background: #222;
      color: #fff;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button id="connectBtn"> Conectar micro:bit</button>
</body>
</html>
```

### `Código desktop/sketch.js`
```js
// public/desktop.js
let scene, camera, renderer, socket;
let starsMesh;
let velocidad = 0;
let brillo = 0.5;
let colorCielo = 0;
let salto = false;

init();
animate();

function init() {
  socket = io();

  scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 2000);
  camera.position.z = 1;

  renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  // Fondo de estrellas
  const geometry = new THREE.BufferGeometry();
  const vertices = [];
  for (let i = 0; i < 8000; i++) {
    vertices.push((Math.random() - 0.5) * 2000);
    vertices.push((Math.random() - 0.5) * 2000);
    vertices.push((Math.random() - 0.5) * 2000);
  }
  geometry.setAttribute("position", new THREE.Float32BufferAttribute(vertices, 3));
  const material = new THREE.PointsMaterial({ color: 0xffffff, size: 1 });
  starsMesh = new THREE.Points(geometry, material);
  scene.add(starsMesh);

  // Luz central
  const light = new THREE.PointLight(0xffffff, 1);
  light.position.set(0, 0, 0);
  scene.add(light);

  // SOCKET EVENTOS
  socket.on("mobile-data", (data) => {
    velocidad = data.velocidad;
    brillo = data.brillo;
    colorCielo = data.colorCielo;
    salto = data.salto;
  });

  socket.on("microbit-data", (data) => {
    camera.rotation.x += data.tiltX * 0.05;
    camera.rotation.y += data.tiltY * 0.05;

    if (data.botonA === 1) {
      console.log("Motores encendidos");
    }
    if (data.botonB === 1) {
      brillo = Math.min(1, brillo + 0.1);
    }
    if (data.shake === 1) {
      console.log("Reinicio de simulación");
      camera.rotation.set(0, 0, 0);
    }
  });
}

function animate() {
  requestAnimationFrame(animate);
  scene.rotation.y += 0.0005 + velocidad * 0.005;
  renderer.setClearColor(new THREE.Color(`hsl(${colorCielo * 360}, 50%, ${brillo * 50 + 10}%)`));
  renderer.render(scene, camera);
}
```

### `Codigo mobile/index.html`

```html
<!-- public/mobile.html -->
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Panel de Vuelo – Interstellar</title>
  <script src="https://cdn.jsdelivr.net/npm/p5/lib/p5.min.js"></script>
  <script src="/socket.io/socket.io.js"></script>
  <script src="mobile.js"></script>
  <style>
    body { margin: 0; background: black; overflow: hidden; }
  </style>
</head>
<body></body>
</html>
```
### `Código mobile/sketch.js`
```js
// public/mobile.js
let socket;
let velocidad = 0;
let brillo = 0.5;
let colorCielo = 0;
let salto = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();

  textAlign(CENTER, CENTER);
  textSize(20);
}

function draw() {
  background(10);
  fill(255);
  text("Panel de Vuelo – Interstellar", width / 2, 40);

  // Palanca de velocidad
  fill(100);
  rect(width * 0.75, 100, 60, height * 0.6);
  fill(200);
  rect(width * 0.75, map(velocidad, 0, 1, height * 0.7, 100), 60, 20);

  // Slider de brillo
  fill(100);
  rect(width * 0.25, 100, 60, height * 0.6);
  fill(200);
  rect(width * 0.25, map(brillo, 0, 1, height * 0.7, 100), 60, 20);

  // Botón salto
  fill(salto ? "red" : "darkred");
  ellipse(width / 2, height * 0.85, 100);

  socket.emit("mobile-data", { velocidad, brillo, colorCielo, salto });
}

function touchMoved() {
  if (mouseX > width * 0.7) velocidad = constrain(map(mouseY, height * 0.7, 100, 0, 1), 0, 1);
  if (mouseX < width * 0.3) brillo = constrain(map(mouseY, height * 0.7, 100, 0, 1), 0, 1);
}

function touchEnded() {
  if (dist(mouseX, mouseY, width / 2, height * 0.85) < 50) salto = !salto;
}
```

### `server.js`

```js
// server.js
const express = require("express");
const http = require("http");
const { Server } = require("socket.io");
const SerialPort = require("serialport");
const { ReadlineParser } = require("@serialport/parser-readline");

const app = express();
const server = http.createServer(app);
const io = new Server(server);

app.use(express.static("public"));

server.listen(3000, () => console.log("Servidor activo en http://localhost:3000"));

// === MICRO:BIT SERIAL ===
const port = new SerialPort({ path: "COM14", baudRate: 115200 }); //
const parser = port.pipe(new ReadlineParser({ delimiter: "\n" }));

parser.on("data", (line) => {
  const parts = line.trim().split(",");
  if (parts.length === 5) {
    const [tiltX, tiltY, botonA, botonB, shake] = parts.map(parseFloat);
    io.emit("microbit-data", { tiltX, tiltY, botonA, botonB, shake });
  }
});

io.on("connection", (socket) => {
  console.log(" Cliente conectado:", socket.id);

  socket.on("mobile-data", (data) => {
    io.emit("mobile-data", data);
  });

  socket.on("disconnect", () => console.log("❌ Cliente desconectado"));
});
```

### `micropython`
```py
from microbit import *

while True:
    tiltX = accelerometer.get_x() / 1024
    tiltY = accelerometer.get_y() / 1024
    a = 1 if button_a.is_pressed() else 0
    b = 1 if button_b.is_pressed() else 0
    shake = 1 if accelerometer.was_gesture("shake") else 0

    # Enviar como línea de texto simple
    print("{},{},{},{},{}".format(tiltX, tiltY, a, b, shake))
```


