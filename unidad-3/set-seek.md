# Unidad 3

## 🔎 Fase: Set + Seek

![Simple Flowchart Infographic Graph](https://github.com/user-attachments/assets/fa3736c0-1a35-4d8f-bac0-6c7d66424002)

**Vectores de prueba:**

| #  | Estado inicial   | Evento/Entrada             | Estado esperado     | Salida/Acción esperada                           |
|----|-----------------|----------------------------|--------------------|-------------------------------------------------|
| 1  | `STATE_CONFIG`  | `A`                        | `STATE_CONFIG`     | `count = min(count+1,60)`; `mostrar(count)`     |
| 2  | `STATE_CONFIG`  | `B`                        | `STATE_CONFIG`     | `count = max(10,count-1)`; `mostrar(count)`     |
| 3  | `STATE_CONFIG`  | `ESPACIO`                  | `STATE_ARMED`      | `startTime = ticks_ms()`; `mostrar(count)`      |
| 4  | `STATE_ARMED`   | `A` (correcto, progreso=0) | `STATE_ARMED`      | `progreso = 1`                                  |
| 5  | `STATE_ARMED`   | `B` (correcto, progreso=1) | `STATE_ARMED`      | `progreso = 2`                                  |
| 6  | `STATE_ARMED`   | `A` (correcto, progreso=2) | `STATE_CONFIG`     | `estado = DESACTIVADA`; `count = 20`; `mostrar(count)` |
| 7  | `STATE_ARMED`   | `B` (incorrecto en progreso=0) | `STATE_ARMED`  | `progreso = 0` (reinicio)                       |
| 8  | `STATE_ARMED`   | `tick` con `count > 0`     | `STATE_ARMED`      | `count--`; `mostrar(count)`                     |
| 9  | `STATE_ARMED`   | `tick` con `count = 0`     | `STATE_EXPLODED`   | `mostrar(SKULL)`                                |
| 10 | `STATE_EXPLODED`| `R`                        | `STATE_CONFIG`     | `count = 20`; `mostrar(count)`; reset           |





