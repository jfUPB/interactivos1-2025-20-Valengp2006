# Unidad 2


## 🤔 Fase: Reflect

### Actividad 06 - 08/08/2025

**Parte 1: recuperación de conocimiento (Retrieval Practice)**

**1) Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?**
  
  Una máquina de estados es un modelo que describe cómo un sistema pasa de un estado a otro en respuesta a una interacción o evento generado. Sus cuatros componentes fundamentales son: estados, eventos, acciones y transiciones.  

**2) Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?**

  La técnica de máquina de estados es útil para gestionar la "concurrencia" ya que no bloquea el programa, como ocurre al usar funciones como *sleep* y por tanto soluciona el problema de bloqueo, sino que permite atender múltiples eventos casi que al mismo tiempo, permitiendo que el micro:bit reaccione casi de inmediato a un evento mientras avanza la cuenta regresiva,

**3) Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?**

  No sé como.

**4) Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.**

  Un **vector de prueba** es  una lista de posibles entradas y resultados esperados que se utilizan para verificar el correcto funcionamiento del programa. Esta herramienta es crucial para verificar que una máquina de estados funciona como se espera ya que evalúa los posibles eventos que pueden ocurrir y la respuesa del programa a ellos.

**Parte 2: reflexión sobre tu proceso (Metacognición)**

**1) ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?**

  Del diseño de la bomba temporizada, me resultó más desafiante crear el diagrama de estados, ya que el pensar y diseñar de cero el diagrama es mucho mas complicado que comenzar a traducirlo al lenguaje del micro:bit, esto debido a que, al usar palabras clave y describir lo que debe hacer cada cosa, su traducción a MicroPython es mucho más sencilla.

**2) Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?**

  Un error que encontré fue que el contador no disminuía adecuadamente, por lo que pensarlo en términos de estados y transiciones me ayudó a encontrar el problema, el cual consistía en que estaba ejecutando la transición en el momento equivocado dentro del ciclo principal, por lo que luego de aislar el problema fue más sencillo resolver el problema.

**3) El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?**

  Para poder abordar este problema comencé programando el estado inicial (CONFIG), luego comencé a probar y añadir las demás funcionalidades de forma gradual para verificar su correcto funcionamiento; de igual forma, para poder lograr hacer que el código funcionara busqué algunas opciones relacionadas que fueran una guía para el ejercicio, aplicandolas luego al contexto según era necesarioa para así finalmente obtener el código final.

**4) Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?**

Creo que podría aplicar el patrón de máquina de estados en un proyecto como un videojuego de aventura, esto para lograr que el personaje cambie entre los estados de caminar, saltar, atacar o estar quieto, dependiento de la situación en la que se encuentre.

### Actividad 07

- Encuentra a un compañero de trabajo.
- Intercambien las URLs de sus bitácoras de aprendizaje.
- Revisa con atención las entradas de tu compañero para las Actividades 04 (diagrama de la bomba) y 05 (código y pruebas).
- Analiza de manera crítica el diseño y la implementación de tu compañero y deja un comentario de retroalimentación específico y constructivo.
- Conversa con tu compañero sobre su diseño y código, y discutan sus comentarios.

[Enlace a la bitácora de mi compañero](https://github.com/jfUPB/interactivos1-2025-20-pinwinasio480/blob/unidad2/apply/unidad-2/apply.md)

**Comentario:** Mi compañero creó una máquina de estados que funciona bastante bien, con transiciones clr¿aras y una buen manejo del tiempo. También, hizo uso de vectores de prueba para probar su correcto funcionamiento; sin embargo, e podría mejorar haciendo la cuenta regresiva un poco más clara evitando código repetitivo y agregando señales especiales al llegar o los límetes o reiniciar la bomba, los cuales agregan un poco más de estética a su bomba temporizada.

### Actividad 08

**1) Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?**

  La actividad de la bomba temporizada me ayudó más a entender el poder de las máquinas de estados, ya que mostró como su implementación puede facilitar 

**2) Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso, innecesariamente complicado o que aportó poco a tu aprendizaje? ¿Qué cambiarías o eliminarías?**

  La Actividad 01 fue la que me pareció más confusa, principalmente debido a que fue el primer ejemplo visto de máquinas de estados, el cual, desde mi punto de vista, fue algo complejo de hacer.

**3) Empezar a hacer: ¿Qué te habría ayudado a entender mejor?**

  Para mi, me hubiera sido de mucha ayuda un poco más de contexto en la parte teórica de las máquinas de estados, esto antes de comenzar con el ejemplo aplicado del tema.

**4) Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa (Actividad 03) al diseño desde cero de uno complejo (Actividad 04 y 05)? ¿Por qué?**

  Desde mi punto de vista sería un 4 en dificultad, ya que es muy diferente el analizar un programa a tener que diseñar uno desde cero, a pesar de las explicaciones y los ejemplos dados en clase, pues al fin y al cabo hay un gran cambio al pasar de análisis a desarrollo.

**5) Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?**

  La parte del diagrama de estados fue lo más frustrante para mi, más aún que el programar en sí, ya que no tenía muy claro que debia poner en cada cosa, ni como debia organizar el diagrama como tal, por lo que su diseño me costó demasiado.



