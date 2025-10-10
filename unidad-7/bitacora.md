# Evidencias de la unidad 7

## Actividad 01 - 08/10/2025

### Procedimiento

1. Se clonó el repositorio del caso de estudio y se abrieron los archivos del proyecto en **Visual Studio Code**.
2. En la terminal del proyecto se ejecutó el comando:

   ```bash
   npm install
   ```

   Esto permitió instalar las dependencias necesarias (`express` y `socket.io`).
   
4. Luego, se ejecutó:

   ```bash
   npm start
   ```

   Al hacerlo, la terminal mostró el mensaje:
   `Server is listening on http://localhost:3000`
   
6. En **VS Code**, se abrió el panel de **PORTS** y se seleccionó “Forward a Port (Dev Tunnels)”, indicando el puerto **3000** y configurando la visibilidad como **Public**.
7. Se copió la URL generada por Dev Tunnels y se envió al celular.
   Por ejemplo:

   ```
   https://p8r9rzpx-3000.use2.devtunnels.ms/
   ```
<img width="1414" height="150" alt="Captura de pantalla 2025-10-10 140234" src="https://github.com/user-attachments/assets/8f5e9210-0c6f-4efa-aa6f-b459fdf2cb44" />

8. Se accedió a las siguientes rutas:

  - En el computador: `https://p8r9rzpx-3000.use2.devtunnels.ms/desktop/`
     <img width="473" height="486" alt="Captura de pantalla 2025-10-10 141041" src="https://github.com/user-attachments/assets/a7daf069-42e9-457b-a99a-90fe780ffb72" />
- En el celular: `https://p8r9rzpx-3000.use2.devtunnels.ms/mobile/`
     ![WhatsApp Image 2025-10-10 at 2 10 56 PM](https://github.com/user-attachments/assets/d05e2363-84ec-4961-896a-ff0512faec55)

9. Finalmente, se probó la interacción táctil desde el celular para mover el círculo en tiempo real en la pantalla del computador.

### Observaciones

<img width="748" height="485" alt="Captura de pantalla 2025-10-10 140742" src="https://github.com/user-attachments/assets/8cc58ced-fd8e-4039-a4d7-1737b82d4444" />

- En la terminal del servidor aparecieron mensajes como:

  ```
  New client connected
  Received message => position data
  Client disconnected
  ```
- Cada cliente (desktop y mobile) fue reconocido con un **identificador distinto (ID de socket)**.
- Al mover el dedo sobre la pantalla del celular, el **círculo rojo del navegador de escritorio** se movía en tiempo real siguiendo la posición táctil.
- No se percibió un retraso notable en la respuesta, indicando una buena sincronización.

### Respuestas a las preguntas

- **¿Qué URL de Dev Tunnels obtuviste?**
  
  `https://p8r9rzpx-3000.use2.devtunnels.ms/`

- **¿Por qué se usa esta URL en lugar de localhost o la IP local?**
  
  Porque `localhost` solo es accesible desde el mismo computador. Dev Tunnels crea una **URL pública segura** que permite acceder al servidor desde otros dispositivos a través de internet, como el celular.

- **¿Qué hace `npm install` y `npm start`?**

  - `npm install`: descarga e instala las dependencias del proyecto.
  - `npm start`: ejecuta el servidor Node.js definido en el archivo `server.js`.

- **¿Qué mensajes observaste en la terminal?**
  
  Aparecieron registros indicando nuevas conexiones, recepción de datos táctiles y desconexiones de clientes.

- **¿Funcionó la interacción?**
  
  Sí. El círculo se movía fluidamente de acuerdo con los movimientos táctiles en el celular. No se detectó latencia significativa.

## Actividad 02 - 10/10/2025

### Explicación del funcionamiento

En esta actividad se buscó comprender cómo es posible que un celular y un computador se comuniquen entre sí en tiempo real a través de Internet usando **Node.js**, **Socket.IO** y **VS Code Dev Tunnels**.

Cuando ejecutamos `npm start`, el servidor Node.js se ejecuta localmente en la dirección **localhost:3000**, que solo es accesible desde el propio computador.
Sin embargo, el celular no puede conectarse a esa dirección, ya que “localhost” en su navegador hace referencia al propio dispositivo móvil.

Para resolver esto, se utiliza **Dev Tunnels**, que crea una **URL pública temporal** (por ejemplo: `https://tulink.use2.devtunnels.ms/`) que actúa como un **intermediario seguro** entre Internet y el servidor local.
Este túnel redirige todo el tráfico que llega desde esa URL pública hasta el puerto 3000 del computador, permitiendo que el celular acceda al servidor local sin necesidad de estar en la misma red Wi-Fi.

### Función `touchMoved()` y el uso del threshold

En el archivo `mobile/sketch.js`, la función `touchMoved()` se ejecuta continuamente cada vez que el usuario **toca y arrastra el dedo sobre la pantalla**.
Dentro de ella, se envían las coordenadas del toque (`mouseX`, `mouseY`) al servidor, que luego las reenvía a la página del escritorio para mover el círculo en tiempo real.

Para evitar saturar la red con demasiados mensajes, se usa una variable llamada **threshold**, que define un **límite mínimo de movimiento** antes de enviar una nueva actualización.
De esta manera, solo se envían datos cuando el dedo realmente se desplaza una distancia significativa, reduciendo la carga de comunicación y mejorando la eficiencia.

### Comparación: Dev Tunnels vs IP local

| Método                     | Ventajas                                                                                                                       | Desventajas                                                                                              |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| **Dev Tunnels**            | Permite conexión desde cualquier red (Wi-Fi o datos móviles). Comunicación cifrada y segura. No requiere configuración de red. | Depende de conexión a Internet. Requiere iniciar sesión en VS Code y mantener el túnel activo.           |
| **IP Local (192.168.x.x)** | Funciona directamente sin intermediarios. Menor latencia al estar en la misma red.                                             | Solo funciona si ambos dispositivos están en la misma red Wi-Fi y no hay bloqueos del router o firewall. |

### Resultados observados

Durante la ejecución:

- El servidor mostró los mensajes **“New client connected”**, **“Received message => …”** y **“Client disconnected”** al cerrar las pestañas.
- Al mover el dedo en el celular, el círculo del escritorio se movió con fluidez, demostrando la correcta transmisión de datos entre ambos clientes a través del servidor Node.js y el túnel público.
- La latencia fue mínima y el sistema respondió en tiempo real.

### Evidencias

**Captura del sistema completo funcionando:**

![Grabación de pantalla 2025-10-10 143024](https://github.com/user-attachments/assets/108d6f8c-5cab-4b67-b722-c94cecf66a53)

![WhatsApp Video 2025-10-10 at 2 31 48 PM](https://github.com/user-attachments/assets/ae27ea14-7a77-4ec4-ba43-a9a0127fb994)


### Conclusión

**Dev Tunnels** permite convertir un servidor local en uno accesible globalmente sin exponer la IP real del computador.
En conjunto con los **eventos táctiles de p5.js**, posibilita una interacción fluida y segura entre dispositivos, demostrando cómo se puede conectar hardware y software en red para experiencias interactivas multiplataforma.
