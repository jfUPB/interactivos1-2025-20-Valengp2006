# Evidencias de la unidad 6
## Actividad 01 - 24/09/2025

### Paso a paso para iniciar el programa

1. Instalar node.js y Git
2. Abrir el repositorio donde está la información
3. En el apartado de `<> Code` buscar la [url](https://github.com/juanferfranco/entangledTest-sfi1-2025-20.git) que termina en `.git` para clonar el repositorio
4. Abrir el `Git Bash`
5. Crear una carpeta para guardar el repositorio usando el comando `mkdir`+ `nombre`
6. Entrar a la carpeta usando el comando `cd` + `nombreCarpeta`
7. Clonar el repositorio usando el comando `git clone` + `direccionRepositorio`
8. Con el comando `code .` entrar a vs code
9. Ejecutar el comando `npm install` en Git Bash
10. Iniciar el programa con el comando `npm start`
    
### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

Cuanod ejecute `npm install` en la terminal apareció la cantidad de "paquetes" (packages) añadidos, y la cantidad de tiempo que le tomó al programa agregarlos, ademas de mostrar la cantidad de vuñnerabilidades que tiene y un comando nuevo en caso de querer buscar mas información sobre pauqetes que buscane el *"funding"*.

<img width="601" height="134" alt="Captura de pantalla 2025-09-24 152744" src="https://github.com/user-attachments/assets/06fe9a54-f0fc-40e4-9e09-05901da15680" />

Creo que su propósito es el de mostrarle al usuario si toda la información del repositorio se clonó correctamente, ya que menciona cuantos *packages* se añadieron.

### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

El mensaje que apareció en la terminal después de ejecutar *npm start* fue el siguiente: 

<img width="592" height="102" alt="Captura de pantalla 2025-09-24 152829" src="https://github.com/user-attachments/assets/4064e5e0-3769-450b-844e-16d7693c1d9a" />

El cual indica que el servidor esta escuchando las instrucciones dadas en el [url](http://localhost:3000) mostrado.

### Describe lo que ves inicialmente en page1 y page2 en tu navegador.

Inicialmente en `page1` muestra el letrero de *esperando conexión*, cuando se abre `page2` se inicia la aplicación en ambas páginas al tiempo.

### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

<img width="725" height="196" alt="Captura de pantalla 2025-09-24 153313" src="https://github.com/user-attachments/assets/c9a472f7-d63f-417f-8f5a-b1737438769f" />

### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

<img width="1794" height="889" alt="Captura de pantalla 2025-09-24 153052" src="https://github.com/user-attachments/assets/288cc17f-b1c5-4913-8fb2-75a932479cb3" />

<img width="1377" height="884" alt="Captura de pantalla 2025-09-24 153409" src="https://github.com/user-attachments/assets/adea53ef-9451-44b5-a934-76dfc2c0e5d1" />

<img width="708" height="532" alt="Captura de pantalla 2025-09-24 153509" src="https://github.com/user-attachments/assets/90ecf7b5-59cb-4e50-97eb-7bde477ad0bc" />

## Actividad 02

### Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.

En mi casa me conecto a Internet mediante el Wi-Fi, a excepción del televisor, el cual está conectado por medio de un cable de red. Si esa rampa se corta, entonces mi "vehículo" quedaría completamente desconectado de la red de carreteras, por lo que al cortarse esa rampa, quedaría completamente incomunicado con el servidor y demás espacios.

### ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

Al pedir comida en un restaurante, el servidor es el mesero, quien recibe la información que pide el usuario; el usuario es el mismo cliente, quien pide lo que desea recibir al servidor. Así, el servidor sabe lo que busca el cliente, lo busca y se lo entrega.

### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

$\color{red}{\text{Protocolo}}$
$\color{green}{\text{Nombre de dominio}}$
$\color{orange}{\text{Ruta específica}}$

URL: https://www.youtube.com/?app=desktop&hl=es

```diff
- https://
+ www.youtube.com
! /?app=desktop&hl=es
```

- Si solo escribo el dominio sin una ruta específica, igual me lleva a la página de inicio del sitio web.
- El servidor me envía por defecto a la página principal del sintio web.

<img width="1919" height="993" alt="Captura de pantalla 2025-09-26 145109" src="https://github.com/user-attachments/assets/745a847d-af55-4ec0-93d8-7cf83a3c7a9f" />
<img width="1919" height="987" alt="Captura de pantalla 2025-09-26 145125" src="https://github.com/user-attachments/assets/e08b5cd5-ad31-4162-84a6-c6a2cf924785" />


### Compara HTTP con los protocolos seriales que usaste.
- **¿Qué similitudes encuentras?**
- **¿Qué diferencias clave ves?**
- **¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?**
  
- **Similitudes:**  
  - Ambos definen un “idioma” con reglas claras entre emisor y receptor.  
  - El cliente (navegador / micro:bit) envía un mensaje, y el servidor/receptor contesta.  

- **Diferencias:**  
  - HTTP es mucho más complejo: incluye cabeceras, códigos de estado, tipos de contenido.  
  - Serial es más directo: solo transmite bytes sin tanta “meta-información”.  

HTTP necesita esta complejidad porque en la web hay **múltiples tipos de datos** (texto, imágenes, video, JSON) y debe asegurar compatibilidad entre millones de clientes y servidores.

### Piensa en una página web simple, como un formulario de login.
- **¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?**
- **¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?**
- **¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?**

Ejemplo: formulario de login

- **HTML:** los campos de texto (usuario, contraseña) y el botón.  
- **CSS:** color del botón, tipo de letra, márgenes y estilos visuales.  
- **JavaScript:** validar que el usuario escribió algo, mostrar un mensaje de error sin recargar la página.

### Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.
- **¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?**
- **¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**

- **draw() en p5.js:** corre constantemente en bucle (~60 fps), incluso si nada cambia.  
- **Modelo de eventos en la web:** el navegador “espera” a que algo ocurra (click, resize, mensaje) y ejecuta la función correspondiente.  

**Ventajas del modelo de eventos:**  

- Más eficiente: no consume recursos redibujando todo sin necesidad.  
- Más natural para interfaces de usuario (solo reaccionan cuando hay interacción).
  
Si la web usara un bucle `draw()` para todo, sería muy pesado y poco práctico.

### ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

Usar el mismo lenguaje (JavaScript) en cliente y servidor es útil porque:  

- Evita que el desarrollador tenga que aprender dos lenguajes distintos.  
- Se pueden **compartir librerías y lógica** (ej. validación de formularios en cliente y servidor).  
- Hace que el flujo de desarrollo sea más rápido y consistente.
  
### Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

- **HTTP tradicional:** es como enviar un correo → cada vez que quiero algo, debo pedirlo y esperar la respuesta.  
- **WebSockets/Socket.IO:** es como abrir una llamada telefónica → la conexión queda abierta, y ambos lados pueden enviarse mensajes en tiempo real.

**Aplicaciones típicas:**  
- Chats en línea (WhatsApp Web, Messenger).  
- Juegos multijugador en tiempo real.  
- Colaboración en vivo (Google Docs, Figma).  
- Monitoreo de sensores en tiempo real (IoT).

## Actividad 03 - 26/09/2025

### Experimento 1:

**Verificación del funcionamiento del programa antes de modificarlo:**

Al ejecutar las pruebas y abrir las páginas **page1** y **page2**, el servidor muestra los siguientes registros en consola:

- Se registran las conexiones de los clientes, cada uno con su **ID único**.
- Los eventos **win1update** y **win2update** se reciben con las coordenadas de la ventana (`x, y, width, height`).
- En los mensajes de depuración (`Debug`) se refleja:
  - Número total de clientes conectados.
  - Estado de las páginas activas (Page1, Page2).
  - Número de clientes sincronizados (`Synced`).
- Finalmente aparece el mensaje **"All clients are fully synced"**, indicando que la sincronización entre ambos clientes fue exitosa.
  
<img width="562" height="226" alt="Captura de pantalla 2025-09-26 153421" src="https://github.com/user-attachments/assets/0ba513f8-89a0-4fb1-9bc5-bb1d9f591212" />

<img width="560" height="198" alt="Captura de pantalla 2025-09-26 153452" src="https://github.com/user-attachments/assets/0de8ed10-3ef6-492e-8594-82ff182d9faf" />

**Experimento 1:**

- Al intentar abrir **`/page1`**, el navegador mostró el mensaje:

<img width="991" height="160" alt="Captura de pantalla 2025-10-01 144345" src="https://github.com/user-attachments/assets/8a47212a-7476-4e02-af42-2595c767a35d" />

- Al abrir **`/pagina_uno`**, la página cargó correctamente (círculo y línea en rojo):

<img width="1452" height="907" alt="Captura de pantalla 2025-10-01 144403" src="https://github.com/user-attachments/assets/92771ec4-57d8-4ebc-b05b-a168054e1c9c" />

- El servidor **no reconoció la ruta antigua (`/page1`)** porque ya no existe en el código.
- Al cambiar la definición de la ruta en el archivo `server.js`, el servidor solo responde a esa ruta exacta:

  ```js
  app.get('/pagina_uno', (req, res) => { ... });
  ```

Esto confirma que **el servidor asocia cada URL exactamente con las rutas definidas en el código**. Si la ruta no existe, responde con el error `Cannot GET`.

### Experimento 2:

Al abrir **`page1`**:

<img width="685" height="86" alt="Captura de pantalla 2025-10-01 145149" src="https://github.com/user-attachments/assets/ff2f8343-2ee1-4396-880d-4279f50d1723" />

Al abrir  **`page2`**:

<img width="712" height="110" alt="Captura de pantalla 2025-10-01 150638" src="https://github.com/user-attachments/assets/5b04cf96-fa33-4cf4-82ad-4508c05b7554" />

Al cerrar **`page1`**:

<img width="313" height="17" alt="Captura de pantalla 2025-10-01 145337" src="https://github.com/user-attachments/assets/430d3e7e-4e47-4a19-afaf-6cbb760513bd" />

Al cerrar **`page2`**:

<img width="313" height="16" alt="Captura de pantalla 2025-10-01 145329" src="https://github.com/user-attachments/assets/3ba7d36c-b547-42ae-84b4-86bfff9b1b22" />

- Cada vez que un cliente se conecta, el servidor asigna un ID único.
- El ID cambia según la pestaña o cliente que se conecte.
- Cuando se cierra una pestaña, la terminal muestra claramente el mensaje de desconexión con el mismo ID asignado a esa conexión, confirmando el seguimiento individual de cada cliente.
- Esto evidencia cómo Socket.IO gestiona múltiples conexiones simultáneas, diferenciando a los clientes por su ID.

### Experimento 3:

Al abrir el programa antes de modificar el código:

<img width="690" height="196" alt="Captura de pantalla 2025-10-01 145822" src="https://github.com/user-attachments/assets/2e7fa029-4aa4-42c3-a7f7-c86b354ca477" />

Luego de haber modificado el código:

<img width="694" height="293" alt="Captura de pantalla 2025-10-01 150337" src="https://github.com/user-attachments/assets/6ba2905a-0a7a-45f0-966e-64d2c141d9f2" />

<img width="1788" height="988" alt="Captura de pantalla 2025-10-01 150040" src="https://github.com/user-attachments/assets/54456b08-4400-40b4-a8bd-c977dab03798" />

- Cada cliente que se conecta envía su información de ventana (posición y tamaño) al servidor.
- El servidor recibe los datos y mantiene un estado compartido que refleja qué clientes están en page1 y en page2.
- En la consola se observa cómo, al conectarse dos clientes, el servidor muestra Page1: 1, Page2: 1 y luego All clients are fully synced, lo que indica que ambos enviaron su información y la sincronización está completa.
- En el navegador, page1 visualiza los dos nodos conectados por una línea (relación entre clientes), mientras que page2 muestra únicamente su propio círculo.
- Esto demuestra cómo el servidor actúa como intermediario entre los clientes, asegurando que compartan estado y mantengan la coherencia en la comunicación en tiempo real.

### Experimento 4:

Al abrir **`http://localhost:3000/page1`**:

<img width="988" height="662" alt="Captura de pantalla 2025-10-01 151810" src="https://github.com/user-attachments/assets/e3e23c64-954e-498b-9a66-472db270f7b3" />

Al abrir **`http://localhost:3001/page1`**:

<img width="994" height="479" alt="Captura de pantalla 2025-10-01 151817" src="https://github.com/user-attachments/assets/b65b0e9a-c65b-4848-9503-d28aec3658fe" />

Al iniciar el servidor con el puerto cambiado a **3001**:

<img width="684" height="87" alt="Captura de pantalla 2025-10-01 151842" src="https://github.com/user-attachments/assets/08cf4979-9132-4419-b4be-3e1d2e8f28ee" />

- Cuando cambiamos la constante `port` a **3001**, el servidor deja de escuchar en `3000` y solo responde en `3001`.
- Esto demuestra que **la variable `port` define dónde escucha el servidor**, y que la función `server.listen(port)` abre la conexión en ese puerto específico.
- Si intentas conectarte a un puerto incorrecto, simplemente no habrá servidor respondiendo.

## Actividad 04 - 01/10/2025

### Experimento 1:


<img width="992" height="382" alt="Captura de pantalla 2025-10-01 153550" src="https://github.com/user-attachments/assets/6e1b5fef-98e8-4260-9199-eaac8fab1924" />
<img width="1917" height="523" alt="Captura de pantalla 2025-10-01 153634" src="https://github.com/user-attachments/assets/92efe4a1-49cf-4b25-8ed1-d65236830283" />
<img width="1916" height="629" alt="Captura de pantalla 2025-10-01 153649" src="https://github.com/user-attachments/assets/8197149a-263c-4d01-a860-a2c75c25be62" />
<img width="1916" height="538" alt="Captura de pantalla 2025-10-01 153711" src="https://github.com/user-attachments/assets/43f02a5f-390f-4948-8d8e-2c1f199b4774" />





