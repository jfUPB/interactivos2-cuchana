#### Actividad 5:

**Resumen del concepto y narrativa :**

Una pasarela interactiva que responde en tiempo real a la fuerza de los pasos de las modelos y ruido del público, los pequeños cosmos (usuarios) se unen para construir el ambiente de la pasarela.

**Inputs detallados :**

| Input | Método de simulación | Comportamiento esperado |
|-|-|-|
| Fuerza de los pasos | noise(tPasos) + sliderMultPasos.value() | Cambios lentos y fluctuantes segun un patrón medio realista |
| Ruido del público | noise(ruido)*5 + random (0.3)+ picoRuido con un botón para generar picos | Es cambiante, el boton es para simular los picos ocasionales de los ruidos naturales|
| Activación de picos de ruido | El botón de simular grito activa la variable picoRuido que decae lentamente con el timepo | Simula los aplausos o gritos repentinos del público |

**Proceso (algoritmo) :**

1. Si la fuerza de los pasos supera el umbral que predefiniré:
   - Se generan multiples estrellitas que emeregen desde el centro de la pantalla, para intentar simular una descarga de enegía.
2. Si el ruido del público es muuuy alto:
   - Se modifica el color de fondo para generar una atmósfera distinta que represente la empción del público.
3. Cada estrella:
   - Tiene una dirección aleatoria, se mueve hacia afuera desde el centro y va desvaneciendo gradualmente.
4. El sistema se actualiza cuadro a cuadro:
   - Las partículas vivas se dibujan y se eliminan cuando llegan a un nivel de transparencia casi que nulo.
  
Lo que busco es que los cambios en los inputs se vean mas suaves, para que sea algo agradable visualmente.

**Outputs detallados :**

|Output|Tipo|Propiedades dinámicas| Relación directa con los inputs|
|-|-|-|-|
|Estrellas visuales| Partículas| Tienen direccion aleatoria, movimiento radial, opacidad que va disminuyendo| Se generan cuando la fuerza de los pasos superan el umbral minimo|
|Fondo del escenario|Color| Cambia de color según la intensidad del ruido y genera mini galaxias | Se altera progresivamente con ruido alto del público |
|Indicadores en pantalla| Elementos gráficos|Rectangulos de tamaño proporcional a cada input |
|Sliders y botón| Interfaz de control| Slider ajusta fuerza de pasos simulada y el botón activa el ruido| Permite manipular los inputs durante las pruebas y simulación|

