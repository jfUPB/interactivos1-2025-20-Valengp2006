# Unidad 3


## 🛠 Fase: Apply

### Corrección Actividad 06 - 05/09/2025

[Enlace a p5.js](https://editor.p5js.org/)

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

