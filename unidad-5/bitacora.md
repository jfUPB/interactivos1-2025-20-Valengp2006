
# Evidencias de la unidad 5

## Actividad 01 - 10/09/2025

**1. Comunicación entre micro\:bit y p5.js**

El **micro\:bit** está enviando continuamente por el puerto serial 4 datos:

* `xValue` → valor del acelerómetro en el eje X.
* `yValue` → valor del acelerómetro en el eje Y.
* `aState` → estado del botón A (1 si está presionado, 0 si no).
* `bState` → estado del botón B.

Estos valores se empaquetan en un texto separado por comas y terminado en salto de línea `\n`.
Ejemplo de lo que envía:

```
120,-456,0,1
```

En el **sketch de p5.js**, se abre el puerto serial y se leen esas líneas de texto, que luego se dividen en una lista de 4 valores.

**2. Estructura del protocolo ASCII usado**

El protocolo es **ASCII** porque todos los datos se convierten a **texto legible** antes de enviarse.

La estructura es:

```
xValue,yValue,aState,bState\n
```

- Los valores están separados por **comas**.
- Cada conjunto de datos termina con un **salto de línea `\n`**.

Esto hace que sea fácil de leer en una terminal, pero menos eficiente, porque enviar `"123"` ocupa 3 bytes en vez de 2 si se mandara como binario.

**3. Lectura de datos en p5.js y transformación**

En el sketch, la lectura ocurre aquí:

```javascript
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}
```

- `port.readUntil("\n")` → lee una línea completa de datos.
- `data.split(",")` → divide en los 4 valores.
- `microBitX` y `microBitY` → se ajustan a coordenadas en la pantalla (centrando el dibujo).
- `microBitAState` y `microBitBState` → convierten el texto `"true"/"false"` en valores booleanos.

**4. Generación de eventos A pressed y B released**

El código que genera los eventos es:

```javascript
function updateButtonStates(newAState, newBState) {
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }

  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```

Lo que hace es **comparar el estado actual** con el estado anterior:

- Si antes A estaba en `false` y ahora está en `true`, se genera un evento **"A pressed"**.
- Si antes B estaba en `true` y ahora está en `false`, se genera un evento **"B released"**.

Así, p5.js puede reaccionar a los cambios de los botones.

**5. Evidencias (capturas de pantalla)**

<img width="984" height="913" alt="20250910_153157" src="https://github.com/user-attachments/assets/60cbfd1c-eadd-4d87-abf1-db5d24a6af5b" />

<img width="1054" height="913" alt="20250910_153759" src="https://github.com/user-attachments/assets/e99c6248-3e15-4848-8159-d7646bb86a4c" />




