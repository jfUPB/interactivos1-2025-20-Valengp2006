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

### Recepción de datos en texto

<img width="1097" height="796" alt="Captura de pantalla 2025-09-12 142620" src="https://github.com/user-attachments/assets/312982ac-8f4e-499b-9f57-e895d1a6ba9c" />

**¿Por qué se ve este resultado?**

Porque los datos que está enviando la micro:bit están en formato binario, no en texto ASCII. El programa intenta interpretarlos como caracteres de texto, pero al no corresponder a letras legibles, aparecen símbolos extraños o "basura" en pantalla.

### Recepción de datos en Todo en HEX

<img width="1099" height="791" alt="Captura de pantalla 2025-09-12 142851" src="https://github.com/user-attachments/assets/d4759962-a96e-4f96-94ed-ec43ddfcf438" />

**¿Por qué se ve este resultado?**

Porque al activar la vista “Todo en Hex”, el programa deja de intentar interpretar los datos como texto y en su lugar muestra directamente el valor hexadecimal de cada byte recibido. Esto permite ver de forma comprensible los datos binarios que están llegando.

**¿Cómo está relacionado con esta línea de código?**

```data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))```

Está relacionado porque esa línea convierte (empaqueta) los valores en un mensaje binario con el formato `>2h2B`, que significa:

- 2h: dos números enteros de 2 bytes cada uno → 4 bytes
- 2B: dos números enteros sin signo de 1 byte cada uno → 2 bytes
- En total: 6 bytes por mensaje.

### ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**

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

### En un protocolo de comunicación binario estoy enviando números enteros positivos y negativos del acelerómetro de un micro:bit. Cuando recibo el dato y lo convierto a entero, a veces obtengo valores mayores a 60000 (por ejemplo, `fb bc` → 64444), pero eso no corresponde a un valor posible del acelerómetro. ¿Por qué pasa esto y cómo puedo obtener el valor correcto?

<img width="1090" height="798" alt="Captura de pantalla 2025-09-12 152124" src="https://github.com/user-attachments/assets/fbe2fba4-3ab5-4de0-9337-90306c98b084" />

Esto sucede porque el programa está **interpretando un número con signo como si fuera sin signo**.

El valor hexadecimal `fb bc` en binario es `1111101110111100`.

- Si se interpreta como **entero sin signo (unsigned)**, su valor decimal es `64444`.
- Pero como el dato realmente representa un **entero con signo de 16 bits (signed short)**, se usa un formato llamado **complemento a dos** para representar los números negativos.

En complemento a dos:

- El bit más significativo (MSB) indica el signo (0 = positivo, 1 = negativo).
- Como en `1111101110111100` el primer bit es 1, el número es negativo.
- Al convertirlo correctamente se obtiene:
  - Invertir bits → `0000010001000011`
  - Sumar 1 → `0000010001000100`
  - Resultado en decimal → `1092`
  - Como era negativo → `-1092`

Entonces, el valor correcto de `fb bc` es **`-1092`**, lo cual sí tiene sentido como lectura del acelerómetro (en mili-g).

**¿Entonces cual es la solución?:** Indicarle al programa que lea esos dos bytes como **entero con signo de 16 bits** (`signed short`). Así la computadora interpretará automáticamente el número en complemento a dos y mostrará el valor correcto (positivo o negativo).

### Experimento: enviar solo cuando se agita

- **¿Cuántos bytes se están enviando por mensaje?**
Se están enviando **6 bytes** por cada mensaje.

- **¿Cómo se relaciona esto con el formato `'>2h2B'`?**
El formato `'>2h2B'` define exactamente cuántos bytes se envían y en qué orden:

- `2h` → indica que se envían 2 números enteros cortos (de 2 bytes cada uno) → 4 bytes en total.
- `2B` → indica que se envían 2 números enteros sin signo (de 1 byte cada uno) → 2 bytes en total.
  **4 + 2 = 6 bytes** por mensaje.
  
Por eso, al observar los datos en hexadecimal, siempre aparecen grupos de 6 bytes por cada mensaje enviado.

**¿Qué significa cada uno de los bytes que se envían?**

* Los **primeros 2 bytes** representan el valor de `xValue` (aceleración en el eje X).
* Los **siguientes 2 bytes** representan el valor de `yValue` (aceleración en el eje Y).
* El **quinto byte** representa el estado de `button_a` (1 si está presionado, 0 si no).
* El **sexto byte** representa el estado de `button_b` (1 si está presionado, 0 si no).

### Valores positivos y negativos en el formato `'>2h2B'`

**¿Cómo se verían esos números en el formato `'>2h2B'`?**
Los valores de `xValue` y `yValue` pueden ser positivos o negativos, y como se envían con el tipo `h` (entero corto con signo), se representan en **complemento a dos** usando 2 bytes cada uno.

* Si el número es **positivo**, el bit más significativo (MSB) es 0 y el valor en hexadecimal aparece normalmente (por ejemplo, `+100` → `00 64`).
* Si el número es **negativo**, el bit más significativo es 1 y el valor aparece como su representación en complemento a dos (por ejemplo, `-100` → `FF 9C`).

Así, aunque se vea un valor “grande” en hexadecimal, en realidad corresponde a un número negativo cuando se interpreta como entero con signo.



