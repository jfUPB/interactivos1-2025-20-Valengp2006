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
  - **4 + 2 = 6 bytes** por mensaje.

Por eso, al observar los datos en hexadecimal, siempre aparecen grupos de 6 bytes por cada mensaje enviado.

**¿Qué significa cada uno de los bytes que se envían?**

* Los **primeros 2 bytes** representan el valor de `xValue` (aceleración en el eje X).
* Los **siguientes 2 bytes** representan el valor de `yValue` (aceleración en el eje Y).
* El **quinto byte** representa el estado de `button_a` (1 si está presionado, 0 si no).
* El **sexto byte** representa el estado de `button_b` (1 si está presionado, 0 si no).

### Valores positivos y negativos en el formato `'>2h2B'`

**¿Cómo se verían esos números en el formato `'>2h2B'`?**

Los valores de `xValue` y `yValue` pueden ser positivos o negativos, y como se envían con el tipo `h` (entero corto con signo), se representan en **complemento a dos** usando 2 bytes cada uno.

- Si el número es **positivo**, el bit más significativo (MSB) es 0 y el valor en hexadecimal aparece normalmente (por ejemplo, `+100` → `00 64`).
- Si el número es **negativo**, el bit más significativo es 1 y el valor aparece como su representación en complemento a dos (por ejemplo, `-100` → `FF 9C`).

Así, aunque se vea un valor “grande” en hexadecimal, en realidad corresponde a un número negativo cuando se interpreta como entero con signo.

**Ejemplo:**

<img width="1090" height="798" alt="Captura de pantalla 2025-09-12 152124" src="https://github.com/user-attachments/assets/fbe03246-8666-4f79-a2ab-21088d515818" />

- El valor hexadecimal fb bc representa un número negativo en un formato estándar llamado complemento a dos.
- El programa lee los bits 1111101110111100 y, al tratarlo como un número sin signo, calcula su valor directo, que es 64,444. Sin embargo, en los números con signo, el primer bit (el más a la izquierda) se usa para indicar si el número es positivo (0) o negativo (1). Como en tu caso empieza con 1, es un número negativo.
- El valor real de fb bc (hexadecimal) corresponde a -1092 en decimal.
- Para obtener el valor correcto, es necesario indicarle al programa que lea esos dos bytes como un entero de 16 bits con signo (en inglés, signed 16-bit integer o short). La computadora aplicará automáticamente el siguiente cálculo (conocido como "complemento a dos"):
    - **Valor Binario:** 1111 1011 1011 1100
    - **Invertir los bits:** 0000 0100 0100 0011
    - **Sumar 1:** 0000 0100 0100 0100
    - **Calcular el valor decimal:** El resultado es 1092.
    - **Añadir el signo negativo:** Como el bit original era 1, el valor final es -1092.

**En resumen:** No es un error en el envío de datos. Simplemente, es necesario asegurarse de que el programa que recibe los datos los interprete como un entero de 16 bits con signo para decodificar correctamente los números negativos.

### ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?

**Diferencias observadas:**

- Los datos en binario aparecen como caracteres raros o símbolos no legibles en la consola, porque son bytes crudos (valores entre 0 y 255).
- Los datos en ASCII aparecen como números legibles separados por comas, por ejemplo: `123,-45,0,1`
- Son texto normal que representa los valores numéricos.

**Ventajas del formato binario (struct.pack):**

- Ocupa menos bytes (solo 6 en este caso: 2 bytes + 2 bytes + 1 byte + 1 byte).
- Es más rápido de enviar y procesar, porque no necesita convertir los números a texto.
- Evita errores por caracteres extra (comas, saltos de línea, etc.).

**Desventajas del formato binario:**

- No es legible para humanos directamente.
- Necesitas saber exactamente el formato para poder interpretar correctamente los bytes recibidos.

**Ventajas del formato ASCII:**

- Es fácil de leer y depurar durante el desarrollo.
- No necesitas conocer un formato especial, basta con separar por comas.

**Desventajas del formato ASCII:**

- Ocupa más bytes (cada número convertido a texto puede ocupar varios caracteres).
- Es más lento de transmitir y procesar, porque implica convertir números a texto y luego volver a números al recibirlos.

#### Evidencia:

<img width="1096" height="796" alt="Captura de pantalla 2025-09-17 144627" src="https://github.com/user-attachments/assets/e59fdd86-8f49-4be1-855d-d58085447080" />

## Actividad 03 - 17/09/2025

### ¿Por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea, y ahora no es necesario?

En la unidad anterior, los datos se enviaban en formato ASCII (texto), donde cada valor numérico era convertido en caracteres (por ejemplo "500,524,1,0\n"). Como el tamaño de cada mensaje podía variar (algunos números tienen 1 dígito, otros 3 o más), el receptor no podía saber dónde terminaba un mensaje y empezaba el siguiente.

Por eso, era necesario:

- Separar los valores con delimitadores (como comas ,) para poder distinguirlos.
- Indicar el final de cada mensaje con un salto de línea \n, para que el receptor supiera que ya recibió el mensaje completo.

Ahora, en cambio, los datos se envían en formato binario usando struct.pack('>2h2B'), lo que siempre genera exactamente 6 bytes por mensaje (2 + 2 + 1 + 1), así que el receptor sabe que cada paquete ocupa 6 bytes exactos. Gracias a esto no hacen falta delimitadores ni saltos de línea, porque el tamaño fijo del paquete permite al receptor dividir el flujo de datos en bloques de 6 bytes.

#### Evidencia: 

<img width="897" height="655" alt="Captura de pantalla 2025-09-17 145856" src="https://github.com/user-attachments/assets/5b89fa8b-410e-4833-aa05-622ff03a845e" />

<img width="896" height="651" alt="Captura de pantalla 2025-09-17 145942" src="https://github.com/user-attachments/assets/44201bdc-9c68-4c4a-b16b-acf4d5c7a616" />

### Cambios importantes del nuevo código con respecto al anterior

**Código anterior — datos como texto (CSV):**

```javascript
let values = port.readLine().split(",");
microBitX = int(values[0]) + windowWidth / 2;
microBitY = int(values[1]) + windowHeight / 2;
microBitAState = values[2].toLowerCase() === "true";
microBitBState = values[3].toLowerCase() === "true";
updateButtonStates(microBitAState, microBitBState);
```

- Los datos venían como una línea de texto: "123,456,true,false".
- Se usaba .readLine() para leer la línea completa.
- Luego .split(",") para separar los valores.
- Cada valor había que convertirlo de texto a número o booleano (int() y comparaciones con "true").

**Código nuevo — datos binarios (>2h2B):**
```javascript
if (port.availableBytes() >= 6) {
  let data = port.readBytes(6);
  if (data) {
    const buffer = new Uint8Array(data).buffer;
    const view = new DataView(buffer);

    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    print(`microBitX: ${microBitX} microBitY: ${microBitY} ...`);
  }
}
```

- Ahora se usan 6 bytes exactos en cada mensaje:
    - 2h → 2 enteros con signo de 2 bytes cada uno → microBitX y microBitY
    - 2B → 2 enteros sin signo de 1 byte cada uno → estados de los botones A y B
- Se usa .readBytes(6) en vez de .readLine().
- Se crea un DataView para interpretar los bytes como números binarios, no como texto.
- Ya no hay que convertir strings a números: directamente se leen los valores binarios correctos.

### ¿Qué ves en la consola? ¿Por qué crees que se produce este error?

Al iniciar el programa en p5.js, en la consola aparece inmediatamente un mensaje de error del tipo Event {isTrusted: true, ...}. Aunque no estaba presionando ninguna tecla, el valor que se muestra en la consola es true. Esto indica que el evento se está activando sin que haya una interacción del usuario, lo cual sugiere que hay un error de framing en el código: probablemente el evento está siendo llamado de forma automática en lugar de esperar a que el usuario lo dispare.

**¿Por qué sucede este error?**

- El micro:bit está enviando datos en bloques exactos de 6 bytes (>2h2B).
- Pero el código de p5.js lee con:
```javascript
if (port.availableBytes() >= 6) {
  let data = port.readBytes(6);
  ...
}
```
Si por alguna razón el flujo serial entrega más o menos de 6 bytes de golpe (por ejemplo, 7, 8, o 11 bytes de una sola vez), el readBytes(6) puede:
  - Leer los últimos 2 bytes del mensaje anterior + los primeros 4 del siguiente, combinándolos incorrectamente.

Esto hace que getInt16 interprete bytes "mezclados" y devuelva valores basura (como 3073). Además, en el código, después de enviar los 6 bytes binarios, el micro:bit también envía texto ASCII ("ASCII:\n..."). Si esos bytes ASCII llegan antes de que se lean los binarios, p5.js podría interpretar bytes de texto como parte de los 6 bytes binarios, generando números absurdos.

#### Evidencia:

<img width="1737" height="818" alt="Captura de pantalla 2025-09-17 152154" src="https://github.com/user-attachments/assets/4895cb4d-56cd-43f7-8380-1a3cc3f25500" />

### Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?

En la consola aparece que el micro:bit se conecta correctamente y luego muestra:

`A pressed`
`microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false`

Esto sucede apenas inicio el programa, aunque no estoy presionando ningún botón.
Esto indica que el código está leyendo datos incorrectos, porque está interpretando como true un valor que no corresponde al estado real del botón.

Creo que este error ocurre porque los 6 bytes que lee el programa no están alineados con los 6 bytes que envía el micro:bit, por lo que se produce un error de sincronización (framing) y los valores llegan desordenados o incompletos.

#### Evidencia:

<img width="1738" height="810" alt="Captura de pantalla 2025-09-17 153100" src="https://github.com/user-attachments/assets/f06671d8-28f3-48d9-9540-da65e252fca8" />

###  ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?

**Cambios que tienen los programas:**

**micro\:bit:**

- Ahora empaqueta los datos en un formato binario con `struct.pack('>2h2B', ...)`, enviando 2 valores de acelerómetro (x, y) como enteros de 16 bits y 2 estados de botones como bytes individuales.
- Se añadió un **byte de cabecera (0xAA)** al inicio de cada paquete y un **checksum (suma de los datos módulo 256)** al final, para detectar errores de sincronización.
- Se fija una **velocidad de transmisión de 115200 baudios** y se envían datos cada 100 ms (10 Hz).

**p5.js:**

- Ahora usa un **buffer (`serialBuffer`)** para acumular los bytes que llegan por el puerto serie.
- Busca el **byte de cabecera 0xAA** para alinear los paquetes y solo procesa cuando hay al menos 8 bytes disponibles.
- Verifica el **checksum** recibido y descarta los paquetes incorrectos.
- Se añadieron funciones para **actualizar el estado de los botones A y B**, generando eventos cuando cambian de estado.
- Se añadió **código para dibujar imágenes SVG o líneas** cuando se presiona el botón A del micro\:bit.

**Lo que se observa en la consola de p5.js:**

- Aparece primero el mensaje:
  `Connected to serial port`
  lo que indica que la conexión serie se abrió correctamente.

- Luego:
  `Microbit ready to draw`
  que significa que el micro\:bit comenzó a enviar datos válidos y el programa ya está en estado de dibujo.

- Después se ven mensajes como:
  `A pressed` / `B released`
  que indican que el código detecta correctamente los cambios en el estado de los botones del micro\:bit.

#### Evidencia

<img width="1736" height="809" alt="Captura de pantalla 2025-09-17 153631" src="https://github.com/user-attachments/assets/f5aebda7-b57a-445f-a4d3-adf6bd6658ab" />

## Actividad 05 - 18/09/2025

**Comparación de Protocolos: ASCII vs. Binario**

En estas dos unidades hemos explorado dos formas de comunicación serial. A continuación, se comparan ambos protocolos aplicados a nuestro proyecto de dibujo con el acelerómetro.

| Aspecto | Protocolo ASCII (Unidad 4) | Protocolo Binario (Unidad 5) | Justificación con Ejemplos del Proyecto |
| :--- | :--- | :--- | :--- |
| **Eficiencia** | **Baja**. Cada número se convierte a texto. El valor `-1023` ocupa 5 bytes ("-", "1", "0", "2", "3"). | **Alta**. Los números se envían en su formato nativo. `-1023` ocupa solo 2 bytes como un entero de 16 bits (`0xFC01`). | El mensaje ASCII `"-1023,512,1,0\n"` puede ocupar hasta 15 bytes, mientras que el paquete binario con framing siempre ocupa **8 bytes fijos**. |
| **Velocidad** | **Más lento**. Al enviar más bytes por mensaje, la transmisión tarda más tiempo. | **Más rápido**. Con mensajes más compactos, se pueden enviar más datos en el mismo período, mejorando la respuesta. | A 115200 baudios, enviar 15 bytes (ASCII) es casi el doble de lento que enviar 8 bytes (binario), lo que resulta en una menor latencia. |
| **Facilidad de Uso y Depuración** | **Alta**. Los datos son legibles en cualquier terminal serial (`"120,-456,0,1"`). Es fácil ver si los valores son correctos a simple vista. | **Baja**. Los datos aparecen como "basura" o en hexadecimal (`AA 01 F4 02 0C...`). Se necesita una herramienta o código para interpretarlos. | En la Actividad 02, vimos que sin la vista hexadecimal, los datos binarios eran incomprensibles. Depurar el ASCII fue tan simple como leer la consola. |
| **Uso de Recursos (CPU)** | **Mayor**. Requiere conversiones constantes: de número a texto en el micro:bit (`format()`) y de texto a número en p5.js (`int()`, `split()`). | **Menor**. El empaquetado (`struct.pack`) y desempaquetado (`DataView`) son operaciones binarias muy eficientes y directas para el procesador. | En p5.js, el código ASCII tenía que hacer `split(',')` y `int()`, que son operaciones con texto. El código binario lee directamente los bytes en números, lo cual es más liviano para el navegador. |

**Análisis del Protocolo Binario y *Framing***

- **¿Por qué fue necesario introducir *framing*?**
  
Fue crucial porque la comunicación serial no garantiza que los datos lleguen en bloques perfectos. Como vimos en los experimentos, el receptor (p5.js) podía empezar a leer a la mitad de un paquete de 6 bytes, mezclando datos del final de un mensaje con el principio del siguiente. Esto causaba **errores de sincronización**, resultando en valores absurdos como `microBitX: 3073`. El *framing* resuelve esto al darle una estructura clara a cada paquete.

- **¿Cómo funciona el *framing*? 🚂**
  - El *framing* funciona como un tren. Define un paquete con partes bien diferenciadas:
    - **Cabecera (*Header*)**: Un byte especial al inicio (`0xAA`), que actúa como la **locomotora**. Le dice al receptor: "¡Aquí empieza un nuevo paquete!".
    - **Datos (*Payload*)**: El contenido real del mensaje (los 6 bytes con los valores del acelerómetro y botones), que son los **vagones de carga**.
    - **Suma de Verificación (*Checksum*)**: Un byte al final que valida la integridad de los datos, como el **vagón de cola o cabús** que confirma que el tren está completo y correcto.

- **¿Qué es un carácter de sincronización?**
  
Es el **byte de cabecera** (`0xAA` en nuestro caso). Es un valor único y predefinido que no debería aparecer (o es muy improbable que aparezca) en los datos. Su única función es actuar como una señal clara de "inicio de paquete" para que el receptor pueda sincronizarse con el flujo de datos.

- **¿Qué es el *checksum* y para qué sirve?**
  
El **checksum** es un código de detección de errores. Se calcula realizando una operación matemática sobre los datos del paquete (en nuestro caso, sumando todos los bytes de datos). Sirve para verificar que los datos no se hayan corrompido durante la transmisión. El emisor envía el *checksum* junto con los datos, y el receptor hace el mismo cálculo. Si los resultados coinciden, el paquete se considera válido; si no, se descarta.

**Análisis del Código en p5.js (`readSerialData`)**

- **`serialBuffer = serialBuffer.concat(newData);`**
  - **¿Qué hace `concat`?** La función `concat` **une o concatena** dos arrays. En este caso, añade los nuevos bytes recibidos (`newData`) al final del array que ya teníamos (`serialBuffer`).
  -  **¿Por qué?** Porque los datos seriales pueden llegar en fragmentos. Podríamos recibir 3 bytes ahora y 10 más en unos milisegundos. `concat` nos permite acumular todos estos fragmentos en un solo lugar (el *buffer*) para poder procesarlos como un flujo continuo.

- **`while (serialBuffer.length >= 8)`**
    - **¿Por qué un bucle que recorre si hay 8 o más bytes?** Porque nuestro protocolo de *framing* define que un paquete completo y válido tiene una longitud **exacta de 8 bytes** (1 de cabecera + 6 de datos + 1 de checksum). Si no tenemos al menos 8 bytes en el buffer, es imposible que tengamos un paquete completo, así que no tiene sentido intentar procesarlo. El bucle se asegura de que solo actuemos cuando tengamos suficientes datos.

- **`if (serialBuffer[0] !== 0xaa)`**
    - **¿Qué significa `0xaa`?** Es la **notación hexadecimal** para el número decimal 170. El prefijo `0x` indica que el número está en base 16. Este es el valor que elegimos como nuestro **carácter de sincronización** o *header*.

- **`serialBuffer.shift(); continue;`**
    - **¿Qué hacen?** Si el primer byte del buffer (`serialBuffer[0]`) no es nuestra cabecera `0xAA`, significa que es un dato inválido o "basura".
        - `shift()`: **Elimina el primer elemento** del array `serialBuffer`.
        - `continue`: **Detiene la iteración actual** del bucle `while` y salta inmediatamente a la siguiente.
    - **¿Por qué?** Esta es la lógica de sincronización. Si no encontramos la "locomotora" (`0xAA`), descartamos el byte (`shift`) y revisamos el siguiente (`continue`), repitiendo el proceso hasta encontrar el inicio de un paquete válido.

- **`if (serialBuffer.length < 8) break;`**
    - **¿Qué hace `break`?** Si encontramos una cabecera `0xAA` pero el buffer todavía no tiene los 8 bytes necesarios para un paquete completo, la instrucción `break` **detiene y sale completamente del bucle `while`**.
    - **¿Por qué?** Para evitar quedar en un bucle infinito y para esperar a que lleguen más datos seriales en el siguiente ciclo del `draw()`. Rompemos el bucle para darle tiempo al buffer a llenarse con el resto del paquete.

- **`slice` vs. `splice`**
    - `let packet = serialBuffer.slice(0, 8);`
    - `serialBuffer.splice(0, 8);`
    - **Diferencia**:
      - `slice(inicio, fin)`: **Copia** una porción del array y la devuelve como un nuevo array, **sin modificar el original**.
        * `splice(inicio, cantidad)`: **Elimina** elementos de un array, **modificando el original**.
    - **¿Por qué se usa `splice` después de `slice`?** Es un proceso de dos pasos:
        1.  Primero, **copiamos** el paquete de 8 bytes a la variable `packet` para poder analizarlo (`slice`).
        2.  Luego, una vez copiado, **eliminamos** esos 8 bytes del buffer principal (`splice`) para que no vuelvan a ser procesados en la siguiente iteración del bucle.

- **`reduce((acc, val) => acc + val, 0)`**
    - **¿Cómo opera `reduce`?** Esta función "reduce" un array a un solo valor. Funciona así:
        - `acc` (acumulador): Guarda el resultado acumulado. Empieza en `0` (el segundo argumento de `reduce`).
        -  `val` (valor actual): Es cada uno de los bytes en `dataBytes`.
        - Para cada byte del array, ejecuta la función flecha `(acc, val) => acc + val`, que simplemente suma el valor actual al acumulador. Al final, devuelve la suma total de todos los bytes. Es una forma elegante y funcional de hacer un bucle para sumar elementos.

- **`if (computedChecksum !== receivedChecksum)`**
    - **¿Por qué se compara el checksum?** Esta es la **verificación de integridad**. Comparamos el `checksum` que nos llegó en el paquete (calculado por el micro:bit) con el que nosotros acabamos de calcular a partir de los datos recibidos.
    - **¿Para qué sirve?** Si los dos valores no son iguales, significa que uno o más bytes de los datos se corrompieron durante la transmisión (por ruido eléctrico, por ejemplo).

- **`continue;` (dentro del if del checksum)**
    - **¿Qué hace `continue` aquí?** Si los checksums no coinciden, `continue` detiene el procesamiento de este paquete corrupto y salta al inicio del bucle `while` para buscar el siguiente paquete.
    - **¿Por qué?** Porque si los datos están corruptos, no tiene sentido intentar interpretarlos. Sería peligroso y podría causar errores en la aplicación. Lo más seguro es descartar el paquete y seguir adelante.

- **`DataView` y la conversión de datos**
    - `let view = new DataView(buffer);`
    - `microBitX = view.getInt16(0);`
    - **¿Qué es un `DataView`?** Un `DataView` es un **intérprete de bajo nivel** para leer datos binarios de un `buffer`. Un buffer es solo una secuencia de bytes sin formato; `DataView` nos permite decirle a JavaScript: "lee los 2 bytes que empiezan en la posición 0 como un entero de 16 bits con signo (`getInt16`)", o "lee el byte en la posición 4 como un entero de 8 bits sin signo (`getUint8`)".
    - **¿Por qué son necesarias estas conversiones?** Porque los datos en el buffer son solo bytes crudos (números entre 0 y 255). No podemos simplemente "tomarlos". Por ejemplo, el valor de `xValue` (`500`) se envía como dos bytes (`0x01` y `0xF4`). Ni `1` ni `244` son `500`. Necesitamos `DataView` para que los combine e interprete correctamente como un solo número de 16 bits (`getInt16`). Es el paso que traduce los bytes binarios a los tipos de datos (números, booleanos) que nuestro programa puede entender y usar.
