# Evidencias de la unidad 6
## Actividad 01 - 24/09/2025

**Paso a paso para iniciar el programa**

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
    
**¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?**

Cuanod ejecute `npm install` en la terminal apareció la cantidad de "paquetes" (packages) añadidos, y la cantidad de tiempo que le tomó al programa agregarlos, ademas de mostrar la cantidad de vuñnerabilidades que tiene y un comando nuevo en caso de querer buscar mas información sobre pauqetes que buscane el *"funding"*.

<img width="601" height="134" alt="Captura de pantalla 2025-09-24 152744" src="https://github.com/user-attachments/assets/06fe9a54-f0fc-40e4-9e09-05901da15680" />

Creo que su propósito es el de mostrarle al usuario si toda la información del repositorio se clonó correctamente, ya que menciona cuantos *packages* se añadieron.

**¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?**

El mensaje que apareció en la terminal después de ejecutar *npm start* fue el siguiente: 

<img width="592" height="102" alt="Captura de pantalla 2025-09-24 152829" src="https://github.com/user-attachments/assets/4064e5e0-3769-450b-844e-16d7693c1d9a" />

El cual indica que el servidor esta escuchando las instrucciones dadas en el [url](http://localhost:3000) mostrado.

**Describe lo que ves inicialmente en page1 y page2 en tu navegador.**

Inicialmente en `page1` muestra el letrero de *esperando conexión*, cuando se abre `page2` se inicia la aplicación en ambas páginas al tiempo.

**¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?**

<img width="725" height="196" alt="Captura de pantalla 2025-09-24 153313" src="https://github.com/user-attachments/assets/c9a472f7-d63f-417f-8f5a-b1737438769f" />

**Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?**

<img width="1794" height="889" alt="Captura de pantalla 2025-09-24 153052" src="https://github.com/user-attachments/assets/288cc17f-b1c5-4913-8fb2-75a932479cb3" />

<img width="1377" height="884" alt="Captura de pantalla 2025-09-24 153409" src="https://github.com/user-attachments/assets/adea53ef-9451-44b5-a934-76dfc2c0e5d1" />

<img width="708" height="532" alt="Captura de pantalla 2025-09-24 153509" src="https://github.com/user-attachments/assets/90ecf7b5-59cb-4e50-97eb-7bde477ad0bc" />

## Actividad 02

**Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.**

En mi casa me conecto a Internet mediante el Wi-Fi, a excepción del televisor, el cual está conectado por medio de un cable de red. Si esa rampa se corta, entonces mi "vehículo" quedaría completamente desconectado de la red de carreteras, por lo que al cortarse esa rampa, quedaría completamente incomunicado con el servidor y demás espacios.

**¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?**

Al pedir comida en un restaurante, el servidor es el mesero, quien recibe la información que pide el usuario; el usuario es el mismo cliente, quien pide lo que desea recibir al servidor. Así, el servidor sabe lo que busca el cliente, lo busca y se lo entrega.

**Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?**

$\color{red}{\text{Protocolo}}$
$\color{blue}{\text{Nombre de dominio}}$
$\color{green}{\text{Ruta específica}}$

URL: https://www.youtube.com/?app=desktop&hl=es

```diff
- https://
+ [www.youtube.com](https://www.youtube.com)
! /?app=desktop&hl=es
```

**Compara HTTP con los protocolos seriales que usaste.**
- **¿Qué similitudes encuentras?**
- **¿Qué diferencias clave ves?**
- **¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?**


**Piensa en una página web simple, como un formulario de login.**
- **¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?**
- **¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?**
- **¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?**


**Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.**
- **¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?**
- **¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**


**¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?**


**Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?**












