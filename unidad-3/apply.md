# Unidad 3


## 🛠 Fase: Apply

### Corrección Actividad 06 - 05/09/2025

[Enlace a p5.js](https://editor.p5js.org/Valengp2006/sketches/wGVQKcr-g)

**Código:**

```javascript
let estado = "inactiva";
let tiempo = 30;
let inicioTiempo;

let secuencia = ["A", "B", "A"];
let contrasena = ["", "", ""];
let indice = 0;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(28);
}

function draw() {
  background(30);

  if (estado === "inactiva") {
    // Fondo
    background(200);
    fill(50);
    ellipse(200, 200, 120, 120);

    // Texto
    fill(0);
    textSize(28);
    text("Tiempo: " + tiempo, 200, 100);
    text("Presiona ESPACIO", 200, 300);
    text("Aumenta (A)  Disminuye (B)", 200, 340);

  } else if (estado === "armando") {
    background(0);

    // Bomba como círculo
    fill(80);
    ellipse(200, 200, 150, 150);

    // Tiempo restante
    let transcurrido = int((millis() - inicioTiempo) / 1000);
    let restante = tiempo - transcurrido;

    fill(255, 0, 0);
    textSize(48);
    text(restante, 200, 200);

    if (restante <= 0) {
      estado = "explotada";
    }

  } else if (estado === "explotada") {
    background(30);

    // Dibujar explosión
    noStroke();
    fill(255, 100, 0);
    ellipse(200, 200, 200, 200);
    fill(255, 200, 0);
    ellipse(200, 200, 140, 140);
    fill(255, 255, 0);
    ellipse(200, 200, 80, 80);

    fill(255);
    textSize(32);
    text("💥 BOOM 💥", 200, 50);
    textSize(20);
    text("Presiona R para reiniciar", 200, 350);

  } else if (estado === "desactivada") {
    background(0, 200, 0);

    // Bomba apagada
    fill(50);
    ellipse(200, 200, 150, 150);

    fill(255);
    textSize(28);
    text("Bomba desactivada", 200, 200);
    textSize(20);
    text("Presiona R para reiniciar", 200, 350);
  }
}

function keyPressed() {
  let tecla = key.toUpperCase(); // 🔹 Normalizamos a mayúscula

  if (estado === "inactiva") {
    if (tecla === " ") {
      estado = "armando";
      inicioTiempo = millis();
      indice = 0;
      contrasena = ["", "", ""];
    } else if (tecla === "A") {
      tiempo = min(60, tiempo + 1);
    } else if (tecla === "B") {
      tiempo = max(10, tiempo - 1);
    }
  } 
  
  else if (estado === "armando") {
    if (tecla === secuencia[indice]) {
      contrasena[indice] = tecla;
      indice++;
      if (indice === secuencia.length) {
        estado = "desactivada";
      }
    } else if (tecla === "A" || tecla === "B") {
      // Si se equivoca, reinicia la clave
      contrasena = ["", "", ""];
      indice = 0;
    }
  } 
  
  else if (
    (estado === "explotada" || estado === "desactivada") &&
    tecla === "R"
  ) {
    estado = "inactiva";
    tiempo = 30;
  }
}
```
### Actividad 07

**Código p5.js:**
```javascript
// ----------------------
// Clase BombTask
// ----------------------
class BombTask {
  constructor() {
    this.estado = "inactiva";
    this.tiempo = 30;
    this.inicioTiempo = 0;
    this.secuencia = ["A", "B", "A"];
    this.contrasena = ["", "", ""];
    this.indice = 0;
  }

  update() {
    background(30);

    if (this.estado === "inactiva") {
      background(200);
      fill(50);
      ellipse(200, 200, 120, 120);
      fill(0);
      textSize(28);
      text("Tiempo: " + this.tiempo, 200, 100);
      text("Presiona ESPACIO", 200, 300);
      text("Aumenta (A)  Disminuye (B)", 200, 340);

    } else if (this.estado === "armando") {
      background(0);
      fill(80);
      ellipse(200, 200, 150, 150);
      let transcurrido = int((millis() - this.inicioTiempo) / 1000);
      let restante = this.tiempo - transcurrido;
      fill(255, 0, 0);
      textSize(48);
      text(restante, 200, 200);
      if (restante <= 0) this.estado = "explotada";

    } else if (this.estado === "explotada") {
      background(30);
      noStroke();
      fill(255, 100, 0);
      ellipse(200, 200, 200, 200);
      fill(255, 200, 0);
      ellipse(200, 200, 140, 140);
      fill(255, 255, 0);
      ellipse(200, 200, 80, 80);
      fill(255);
      textSize(32);
      text("💥 BOOM 💥", 200, 50);
      textSize(20);
      text("Presiona R para reiniciar", 200, 350);

    } else if (this.estado === "desactivada") {
      background(0, 200, 0);
      fill(50);
      ellipse(200, 200, 150, 150);
      fill(255);
      textSize(28);
      text("Bomba desactivada", 200, 200);
      textSize(20);
      text("Presiona R para reiniciar", 200, 350);
    }
  }

  handleKey(tecla) {
    tecla = tecla.toUpperCase();
    if (this.estado === "inactiva") {
      if (tecla === " ") {
        this.estado = "armando";
        this.inicioTiempo = millis();
        this.indice = 0;
        this.contrasena = ["", "", ""];
      } else if (tecla === "A") {
        this.tiempo = min(60, this.tiempo + 1);
      } else if (tecla === "B") {
        this.tiempo = max(10, this.tiempo - 1);
      }
    } else if (this.estado === "armando") {
      if (tecla === this.secuencia[this.indice]) {
        this.contrasena[this.indice] = tecla;
        this.indice++;
        if (this.indice === this.secuencia.length) this.estado = "desactivada";
      } else if (tecla === "A" || tecla === "B") {
        this.contrasena = ["", "", ""];
        this.indice = 0;
      }
    } else if ((this.estado === "explotada" || this.estado === "desactivada") && tecla === "R") {
      this.estado = "inactiva";
      this.tiempo = 30;
    }
  }
}

// ----------------------
// Clase SerialTask (polling)
// ----------------------
class SerialTask {
  constructor() {
    this.latestData = "";
    this.connected = false;
  }

  connect() {
    webSerial.requestPort().then(() => {
      webSerial.open({ baudrate: 115200 }).then(() => {
        this.connected = true;
        console.log("Micro:bit conectado ✅");
      });
    });
  }

  update() {
    if (this.connected) {
      let inString = webSerial.readLine();
      if (inString) {
        this.latestData = inString.trim().toUpperCase();
        if (typeof bomb !== "undefined") bomb.handleKey(this.latestData);
      }
    }
  }
}

// ----------------------
// Clase ButtonTask (teclado)
// ----------------------
class ButtonTask {
  constructor() {}
  update() {}
  handleKey(tecla) {
    if (typeof bomb !== "undefined") bomb.handleKey(tecla);
  }
}

// ----------------------
// Variables globales
// ----------------------
let bomb;
let serialTask;
let buttonTask;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(28);

  bomb = new BombTask();
  serialTask = new SerialTask();
  buttonTask = new ButtonTask();

  // Botón de conexión al micro:bit
  let connectBtn = createButton("Conectar micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(() => serialTask.connect());
}

function draw() {
  bomb.update();
  serialTask.update();
  buttonTask.update();
}

// ----------------------
// KeyPressed p5.js
// ----------------------
function keyPressed() {
  if (buttonTask) buttonTask.handleKey(key);
}
```

[Enlace p5.js](https://editor.p5js.org/Valengp2006/sketches/wcEZLrrN_)

**Código Micro:bit:**
```python
from microbit import *

display.show(Image.HAPPY)

class SerialRemote:
    def __init__(self):
        uart.init(baudrate=115200)

    def update(self):
        if button_a.was_pressed():
            uart.write("A\n")
        if button_b.was_pressed():
            uart.write("B\n")
        if accelerometer.was_gesture("shake"):
            uart.write(" \n")  # espacio = iniciar bomba
        if pin_logo.is_touched():
            uart.write("R\n")  # reiniciar bomba

serialRemote = SerialRemote()

while True:
    serialRemote.update()
```


