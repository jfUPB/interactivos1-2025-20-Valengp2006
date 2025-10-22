# Evidencias de la unidad 8

## Actividad 01 - 22/10/2025


### Tema musical

**“Main Theme – Interstelar” – Hans Zimmer**

La composición transmite la inmensidad del universo y la dualidad entre lo humano y lo cósmico. Esta experiencia interactiva busca recrear ese sentimiento de asombro y conexión emocional mediante una simulación inmersiva que combina sonido, luz y movimiento en tiempo real.

### Concepto general de la experiencia

La aplicación propone una **exploración interactiva del espacio exterior**, ambientada con el tema principal de *Interstelar*.
El usuario se convierte en el **piloto de una nave interestelar**, controlando su trayecto a través de un entorno 3D lleno de estrellas, nebulosas y planetas generados mediante **Three.js**, mientras interactúa con una **consola de vuelo táctil** creada en **p5.js** y un **micro:bit** que actúa como dispositivo físico complementario.

El objetivo es crear una experiencia **multiplataforma sincronizada** entre dispositivos, donde cada uno cumple un rol dentro del sistema interactivo:

- **Celular:** interfaz visual y táctil (panel de control).
- **Micro:bit:** control físico con botones y sensores.
- **Computador:** entorno inmersivo tridimensional y visualización de respuestas en tiempo real.

### Referentes visuales y conceptuales

1. [Video de Universo 360](https://www.youtube.com/watch?v=kMVV6YjaGM4)
2. [Viaje 360 por el Sistema Solar](https://www.youtube.com/watch?v=xdURfh5OPjQ)
3. [Película *Interestelar*](https://www.netflix.com/co/title/70305903)
4. Controlador de nave espacial:
<img width="626" height="403" alt="image" src="https://github.com/user-attachments/assets/40c8ed55-bc59-409c-9457-0979b202a8c2" />


### Concepto de interacción

#### Micro:bit – Control físico principal

| Elemento         | Función                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------- |
| **Botón A**      | Enciende o apaga los motores de la nave (activa/pausa la música y los efectos visuales). |
| **Botón B**      | Modifica la intensidad o tonalidad de la iluminación general.                            |
| **Shake**        | Reinicia la simulación a su estado inicial.                                              |
| **Acelerómetro** | Control de dirección: al inclinar el micro:bit, la nave gira o asciende en el espacio.   |

#### Celular – Consola de vuelo táctil (p5.js)

El panel fue diseñado en **p5.js** con inspiración en las consolas de vuelo espaciales vistas desde arriba, similar a la referencia visual mostrada.
Cada elemento del panel cumple una función específica dentro de la experiencia:

| Elemento                             | Función                                                                      |
| ------------------------------------ | ---------------------------------------------------------------------------- |
| **Palanca principal (derecha)**      | Control de velocidad de la nave (acelerar o desacelerar).                    |
| **Palancas secundarias (izquierda)** | Ajuste de rotación y orientación.                                            |
| **Deslizadores**                     | Controlan la intensidad de efectos visuales (nebulosas, brillo, partículas). |
| **Botón triangular rojo**            | Inicia la secuencia de salto interestelar (transición de escena).            |
| **Botones verdes**                   | Cambian el color del cielo o los efectos atmosféricos.                       |
| **Pantalla central**                 | Indica el estado del sistema (velocidad, energía, color activo).             |

El panel se comunica con el computador mediante **Socket.IO**, enviando y recibiendo datos en tiempo real para modificar los parámetros del entorno visual y la música.

#### Computador – Entorno inmersivo 3D (Three.js)

La visualización principal está desarrollada en **Three.js**, y representa un **viaje espacial en primera persona**.
El entorno incluye:

- **Simulación de estrellas y nebulosas dinámicas.**
- **Reactividad visual al audio:** el ritmo y volumen del tema de *Interstellar* afectan el movimiento de partículas y la iluminación.
- **Eventos interactivos:** al presionar el botón rojo o aumentar la velocidad, se ejecutan efectos visuales como distorsión o “salto cuántico”.
- **Sincronización total:** los comandos enviados desde el celular y el micro:bit modifican en tiempo real el entorno 3D.

### Flujo de comunicación del sistema

```text
┌─────────────┐          ┌──────────────┐          ┌─────────────┐
│  micro:bit  │──UART──▶│   Servidor   │◀──socket──│   Celular   │
│ (botones y  │          │ Node.js +    │──socket──▶│ (panel táctil)│
│ acelerómetro)│          │ Socket.IO    │          └─────────────┘
└──────┬──────┘          └──────┬───────┘
       │                        │
       ▼                        ▼
 ┌────────────────────────────────────┐
 │       Cliente de Escritorio        │
 │ (Three.js + p5.js visuales 360°)  │
 │      + música “Interstellar”      │
 └────────────────────────────────────┘
```

Cada dispositivo funciona como un módulo dentro del ecosistema:

- **Micro:bit:** entrada física (hardware).
- **Celular:** interfaz táctil (UI).
- **Computador:** procesamiento visual (render 3D).
- **Servidor Node.js:** puente de comunicación entre los tres.

### Diseño visual y experiencia

1. **Panel táctil móvil:**
   Creado con p5.js, su diseño combina botones, sliders y palancas en vista cenital. Cada elemento reacciona visualmente al tacto mediante animaciones y luces suaves, reforzando la sensación de control real.

2. **Micro:bit:**
   Se sostiene con la mano no dominante y permite controlar la dirección de la nave. Su vibración o respuesta lumínica podría indicar acciones clave (inicio, pausa, salto interestelar).

3. **Pantalla del computador:**
   Muestra un entorno espacial inmersivo en Three.js, donde la música guía el movimiento de las partículas y el brillo del entorno. El usuario percibe cómo cada acción física o táctil altera la composición visual, creando una **sincronía sensorial entre luz, sonido y control**.

### Conclusión

Esta experiencia combina **interacción tangible y digital**, explorando cómo diferentes medios (hardware, touch y visual 3D) pueden integrarse en una narrativa emocional.
A través del lenguaje visual y sonoro de *Interstellar*, el usuario experimenta el control de una nave espacial en un viaje simbólico que une **tecnología, música y emoción** en tiempo real.

