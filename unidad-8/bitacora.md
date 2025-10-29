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

`Código desktop/index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Simulación 3D Controlada por Micro:bit</title>

  <!-- Three.js (asegúrate de usar la versión correcta) -->
  <script src="https://cdn.jsdelivr.net/npm/three@0.152.0/build/three.min.js"></script>

  <!-- Socket.IO (servida por tu servidor Node) -->
  <script src="/socket.io/socket.io.js"></script>

  <!-- Tu script principal -->
  <script defer src="sketch.js"></script>

  <style>
    body {
      margin: 0;
      overflow: hidden;
      background-color: #000;
      font-family: sans-serif;
      color: white;
    }

    canvas {
      display: block;
    }

    #status {
      position: absolute;
      top: 10px;
      left: 10px;
      font-size: 14px;
      background: rgba(0,0,0,0.5);
      padding: 8px 12px;
      border-radius: 8px;
    }
  </style>
</head>
<body>
  <div id="status">Conectando con micro:bit...</div>
</body>
</html>
```

`Código desktop/sketch.js`
```js
// public/desktop/sketch.js
const socket = io();

let scene, camera, renderer, cube, light;

const statusEl = document.getElementById('status');
socket.on('connect', () => statusEl.textContent = '🟢 Conectado al servidor');
socket.on('disconnect', () => statusEl.textContent = '🔴 Desconectado');

function init() {
  scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

  renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  const geometry = new THREE.BoxGeometry();
  const material = new THREE.MeshStandardMaterial({ color: 0x0077ff });
  cube = new THREE.Mesh(geometry, material);
  scene.add(cube);

  light = new THREE.PointLight(0xffffff, 1, 100);
  light.position.set(5, 5, 5);
  scene.add(light);

  camera.position.z = 3;

  animate();
}

function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}

socket.on('microbit-data', (data) => {
  // Acelerar con acelerómetro
  cube.rotation.x = data.y / 500;
  cube.rotation.y = data.x / 500;

  // Botón A cambia color
  if (data.a) cube.material.color.set(0xff0000);

  // Botón B cambia color
  if (data.b) cube.material.color.set(0x00ff00);

  // Shake → reiniciar
  if (data.shake) {
    cube.rotation.x = 0;
    cube.rotation.y = 0;
    cube.material.color.set(0x0077ff);
  }
});

init();
```

`server.js`
```js
// server.js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const { SerialPort } = require('serialport');
const { ReadlineParser } = require('@serialport/parser-readline');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

// Servir los archivos de la carpeta "public"
app.use(express.static('public'));

// --- CONFIGURACIÓN DEL PUERTO SERIAL ---
const serialPort = new SerialPort({
  path: 'COM14', 
  baudRate: 115200
});

const parser = serialPort.pipe(new ReadlineParser({ delimiter: '\n' }));

parser.on('data', (data) => {
  const parts = data.trim().split(',');
  if (parts.length === 5) {
    const [x, y, a, b, shake] = parts.map(Number);
    const json = { x, y, a: Boolean(a), b: Boolean(b), shake: Boolean(shake) };
    console.log('Microbit:', json);
    io.emit('microbit-data', json);
  } else {
    console.error('Formato no válido:', data);
  }
});

io.on('connection', (socket) => {
  console.log('Cliente conectado');

  socket.on('disconnect', () => {
    console.log('Cliente desconectado');
  });
});

server.listen(port, () => {
  console.log(`🌐 Servidor disponible en http://localhost:${port}`);
});
```

`micropython`
```py
from microbit import *
import microbit

while True:
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    a = button_a.is_pressed()
    b = button_b.is_pressed()
    shake = accelerometer.was_gesture('shake')

    # Enviar en formato: x,y,a,b,shake
    print("{},{},{},{},{}".format(x, y, int(a), int(b), int(shake)))
    sleep(100)
```

