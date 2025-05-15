#### Actividad 5

- Describe al menos un error o comportamiento inesperado significativo que encontraste durante las pruebas.
  Cuando el valor de entrada superaba cierto umbral, el objeto visual desaparecía por completo de la pantalla, a pesar de que solo debía cambiar su color o tamaño.

  Escenario “¿Qué pasaría si?”

  - ¿Qué pasa si la aceleración del micro:bit (o mouseY) es extremadamente alta?

  - Se esperaba que solo cambiara el color, pero en vez de eso el objeto desaparecía.

- Explica cómo utilizaste console.log u otras técnicas para identificar la causa de ese error. (estos debugs los quite)
  console.log("Valor de entrada (intensidad):", intensidad);

- Muestra el fragmento de código antes y después de la corrección (o explica claramente el cambio realizado).
  Antes: let size = intensidad * 10;
  Despues: let size = constrain(intensidad * 10, 10, 200);
