# Unidad 1

## 🤔 Fase: Reflect

### Actividad 07: 25/07/2025

#### Parte 1: recuperación de conocimiento (Retrieval Practice)

**1) Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.**

  Las caractrísticas que definen a un sistema físico interactivo son: la presencia de dispositivos de entrada (*input*), proceso (*process*) y dispositivos de salida (*output*).
   
**2) Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?**

**En micro:bit**                  
- Input:                       
  * Botón "A"                    
  * Botón"B"
  * Serial
- Proceso:                     
  
- Output:                      
  *                               

**En p5.js**
- Input:
  * Serial
-Proceso:

- Output:
  * Pantalla

**3) ¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?**

  La función de la línea uart.write('A') en el código del micro:bit lee el botón con la letra A del dispositivo (micro:bit)

  En p5.js no recuerdo el nombre de la función que se encarga de escuhar el mensaje.
   
**4) ¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?**

  La diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo se encuentra en el medio en el cual se realiza ese diseño. Por un lado, en el diseño tradicional, el artista de forma manual realiza cada trazo en un lienzo; mientras que, por otro lado, en el arte generativo se hace uso de máquinas        sitemas parcialmente autónomos, los cuales siguen las instrucciones dadas por el artista y genera una obra.

**5) Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.**

  Para hacer que un circulo en p5.js cambie a un color aleatorio cada vez que se sacude el micro:bit, primero es necesario programar el micro:bit en el editor para  que reaccione a la acción de sacudida (shake); luego, en el p5.js, añadir la biblioteca de micro.bit y comenzar a escribir el código que permita está acción. Para el código en p5.js, es necesario primero crear la figura, luego añadir la función que permite concectarse al micro:bit y ahí usar la función *Random*, asignarla al color de la figura y vincularla al estimulo *Shake* del micro:bit para que funcione correctamente.

**Parte 2: reflexión sobre tu proceso (Metacognición)**

**1) ¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?**

  Para mi lo más desafiante de esta unidad fue la parte técnica, ya que de por sí siempre se me ha dificultado la parte aplicativa de las materias que la parte teórica, esto debido también a que soy algo lenta para entender como funciona el proceso, y hasta no lograr enteder al 100% como hacerlo paso a paso me bloqueo y no logro avanzar en los ejercicios, lo que me dificulta bastante la aplicación práctica de la teoría.

**2) Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?**

  Lo que logré entender en ese instante es que el código en el micro:bit editor y en el p5.js esta directamente relacionados si trabajas con ese dispositivo (micro:bit) ya que si en el editor pusiste de forma incorrecta la interpretación del estímulo que recibe no va a funcionar en el p5.js, por lo que es importante verificar primero el editor y luego si continuar con el código para el diseño.

**3) Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?**

  Después de experimentar y contruir mi primer prototipo, considero que este curso me sirve para aprender más sobre como conectar una interfaz física a un medio digital, e integrarlos de tal forma que a futuro me sea posible diseñar una interfaz que conecte al usuario con el diseño y le permita ser parte del mismo.

**4) El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?**

  Prefiero este tipo de aprendizaje, guiado paso a paso, ya que me permite ir identificando como funciona el programa y ganar confianza poco a poco para finalmente poder desarrollar un ejercicio sola, ya habiando logrado resolver un ejemplo guiado en el cual basarme para aclarar mis dudas sobre como debe funcionar el programa.

### Actividad 08:

- Encuentra un compañero de trabajo.
- Intercambien las URLs de sus bitácoras de aprendizaje.
- Concéntrate en la Actividad 06: control de movimiento con micro:bit de tu compañero. Lee su código (Python y JavaScript).
- Tu compañero resolvió el problema de manera diferente a ti, qué hizo diferente, qué aprendiste de su solución. En tu bitácora documenta lo anterior y escribe, como si le estuvieras explicando, lo que tú hiciste y por qué es diferente a lo que hizo tu compañero.



### Actividad 09:

**1) Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?**

  El video de esta unidad que me resultó más inspirador y me ayudó a entender mejor el potencial de los sistemas físicos interactivos, fue el video en el que se mostró una sala interactiva en la que, a través de los movimientos de la artista sobre una máquina, iban apareciendo nuevos patrones proyectados en la sala de diferentes formas y colores.

**2) Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?**

  La parte de aplicación práctica de los visto me parecio ago confusa y dificil de entender, principalmente debido también a que al haber tenido que ver la clase de forma virtual durante una semana uno varias cosas que no pude hacer, como la primera vez que se conectó el micro:bit al computador, ya que no contaba con los materiales en el momento, por lo que tardé más en ese proceso cuando retome clases de forma presencial y comencé a hacer las actividades.

**3) Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?**

  Me genera más curiosidad ahora el ver más ejemplos de proyectos artísticos, ya que en ese aspecto soy más visual, por lo que me interesa poder ver que otros proyectos existen sobre el tema.

**4) Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?**

  Ver los videos inspiradores de la *Actividad 01* me permitió ver un poco sobre lo que podría llegar a hacer al momento de aplicarlo en a parte técnica durante las *Actividades 03-06*, sin embargo el choque siempre fue algo grande al descubrir que no es tan sencillo como parece, pero es algo que se logrará a través de la práctica.

**5) Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?**

  No tengo más comentarios sobre mi experiencia en esta unidad introductoria.

