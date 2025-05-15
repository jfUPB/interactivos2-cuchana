Si necesitas simulación: documenta tu plan detallado (inputs a simular, método por input, comportamiento esperado, opcionalmente activación/desactivación).

Inputs a simular: 
- Fuerza y frecuencia de pasos de la modelo
- Rudio del público


  Mi plan para simularlo:

  Pasos de modelo:
  - Metodo para simular: Voy a usar noise() para crear valores entre 0 y 1, lo cual despues lo multiplicare por 10 para simular fuerzas variadas, quedaria fuerza = noise(t)* 10; t+=0.01      -
  - Comportamiento esperado: Cambios lentos y continuos para simular una caminata natural, permitira ver como responde el sistema visual a las distintas pisadas
  - Control manual (lo pondré como opcion para poder visualizar mejor los cambios): Un slider en pantalla que permita modificar el factor por el cual se multiplica en tiempo real.
 
  Ruido del público:
  - Metodo para simular: Se simulará con random() y noise() para lograr esos picos ocasionales
  - Comportamiento esperado: Flujo base suave pero con saltos para simular aplausos o gritos, porque se usaran más que todo los picos para afectar los visuales
  - Botón de ruido: para simular un pico de ruido externo
Activación de la simulación
Se incluirá una variable booleana (usarSimulacion) para permitir activar o desactivar la simulación según se desee probar con datos artificiales o reales.
  
