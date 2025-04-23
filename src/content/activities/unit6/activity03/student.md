#### Actividad 3

Para cada uno de los 4 escenarios (“Inputs Extremos”, “Cambio de Parámetro”, “Combinación de Inputs”, “Falla de Input”):
- Describe el escenario específico que estás considerando para tu proyecto.
- Explica el comportamiento que esperas de tu algoritmo y los outputs resultantes.
- Reflexiona brevemente si ese comportamiento es deseable o si revela algo que necesitas ajustar en tu diseño IPO.

Escenario 1: Inputs externos 

- Escenario: El público interactúa de forma intensa, ya sea con muchos aplausos, gritos o exagerado ruido por murmullos, y las modelos tambien caminan muy fuerte o rapido.
- Comportamiento esperado del algoritmo: El sistema genera visuales muy intensos y un estallido visual que lo hace ver pesado y desordenado, las formas estan cambiando rapidamente y los colores se saturan.
- ¿Es deseable?: Puede serlo si queremos que se refleje ese dramatismo en algunos momentos, pero si es constante lo que va a hacer es saturar a los usuarios y dañar la experiencia puesto que con tantas cosas ocurriendo se deja de entender que estan alterando ellos, entonces creo que se podria hacer una correccion donde se establezca un limite de intensidad

Escenario 2: Cambio de parámetro interno

- Escenario: Se modifica el algoritmo de procesamiento para que la sensibilidad al ruido del público se duplique
- Comportamiento esperado del algoritmo: Incluso niveles minimos de ruido disparan las reacciones en los visuales, haciendo que cambien super rapido y que la experiencia salga de control
- ¿Es deseable?: No, le restaria control al sistema y a la experiencia, vuelve todo impredecible y le puede quitar sentido a las acciones y su inlfuencia en el storytelling

Escenario 3: Combinación de inputs

- Escenario: Moselo con pasos muy suaves y lentos, público muy bulloso y control en modo tranquilidad
- Comportamiento esperado del algoritmo: Creeria que seria confuso para el algoritmo porque el publico le dice: tengamos visuales intensos, mientras el control y las modelos quieren mantener calma
- ¿Es deseable?: Si no es premeditado se veria como un erro, si se prepara este escenario para darle prioridad a un input seria chevere para la narrativa creando un balance entre los inputs

Escenario 4: Falla de input
- Escenario: Se pierde la señal del micrófono del público o el sensor de pasos deja de enviar datos
- Comportamiento esperado: El sistema podría congelar los visuales o mantenerse en su último estado. Alternativamente, podría caer en un estado predeterminado (ej: paisaje neutro y poco dinámico).
- ¿Es deseable?: No, seria horrible que se congele sin explicación. Lo mejor sería que el sistema tuviera un estado de contingencia: detectar la falla y mostrar visuales suaves o usar inputs secundarios mientras se recupera la señal.
