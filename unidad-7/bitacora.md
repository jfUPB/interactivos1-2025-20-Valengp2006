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


