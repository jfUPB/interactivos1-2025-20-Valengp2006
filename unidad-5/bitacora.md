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

[Enlace a p5.js](https://editor.p5js.org/Valengp2006/sketches/cL_gV1GeF)

**5. Evidencias (capturas de pantalla)**

<img width="984" height="913" alt="20250910_153157" src="https://github.com/user-attachments/assets/60cbfd1c-eadd-4d87-abf1-db5d24a6af5b" />

<img width="1054" height="913" alt="20250910_153759" src="https://github.com/user-attachments/assets/e99c6248-3e15-4848-8159-d7646bb86a4c" />

## Actividad 02 - 12/09/2025

- **Recepción de datos en texto**

<img width="1097" height="796" alt="Captura de pantalla 2025-09-12 142620" src="https://github.com/user-attachments/assets/312982ac-8f4e-499b-9f57-e895d1a6ba9c" />

**¿Por qué se ve este resultado?**

Porque los datos que está enviando la micro:bit están en formato binario, no en texto ASCII. El programa intenta interpretarlos como caracteres de texto, pero al no corresponder a letras legibles, aparecen símbolos extraños o "basura" en pantalla.

- **Recepción de datos en Todo en HEX**

<img width="1099" height="791" alt="Captura de pantalla 2025-09-12 142851" src="https://github.com/user-attachments/assets/d4759962-a96e-4f96-94ed-ec43ddfcf438" />

**¿Por qué se ve este resultado?**

Porque al activar la vista “Todo en Hex”, el programa deja de intentar interpretar los datos como texto y en su lugar muestra directamente el valor hexadecimal de cada byte recibido. Esto permite ver de forma comprensible los datos binarios que están llegando.

**¿Cómo está relacionado con esta línea de código?**

```data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))```

Está relacionado porque esa línea convierte (empaqueta) los valores en un mensaje binario con el formato `>2h2B`, que significa:

- 2h: dos números enteros de 2 bytes cada uno → 4 bytes
- 2B: dos números enteros sin signo de 1 byte cada uno → 2 bytes
- En total: 6 bytes por mensaje.

**¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**

- **Ventajas del binario:**

  - Ocupa menos espacio (menos bytes por cada dato enviado).
  - Se transmite más rápido, porque los mensajes son más cortos.
  - Es más eficiente para enviar datos numéricos grandes o complejos.

- **Desventajas del binario:**

  - No es legible para humanos (no se pueden interpretar fácilmente a simple vista).
  - Es necesario conocer el formato exacto (>2h2B en este caso) para poder decodificarlo correctamente.
  - Si hay un error en el orden o el tamaño de los datos, es más difícil detectarlo que en ASCII.

- **Ventajas del ASCII (texto)**

  - Fácil de leer y entender por personas.
  - No necesita un formato de decodificación específico, basta con abrir el puerto serie.

- **Desventajas del ASCII**

  - Ocupa más espacio que el binario (más bytes para representar el mismo número).
  - Es más lento de transmitir.


