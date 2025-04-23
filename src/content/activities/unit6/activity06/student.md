#### Actividad 6

1. Claridad y definición
Siento que mi diseño es mayormente claro y específico. Los inputs están bien definidos, con métodos de simulación concretos y rangos funcionales pensados para probar el comportamiento del sistema. El proceso describe claramente cómo reaccionan los visuales ante los cambios en los inputs.
Sin embargo, hay una parte que podría afinarse más: los criterios exactos para la generación de estrellas (por ejemplo, cuántas se generan por cada unidad de fuerza). Esta parte aún se siente un poco vaga porque no he hecho pruebas en código para definir si es mejor generar 5, 10 o 50 partículas por evento. Aún necesito ajustar esos parámetros para que el resultado sea visualmente fluido pero no saturado.

2. Coherencia narrativa
Sí, el flujo IPO que diseñé logra contar la historia que me propuse: una pasarela viva que reacciona al paso de las modelos y al entusiasmo del público. La relación causa-efecto está presente: cada paso genera estrellas, y el ruido transforma la atmósfera visual.
No encuentro una gran desconexión narrativa, aunque podría explorar más formas en que los outputs expresen emociones distintas dependiendo del tipo de reacción del público. Tal vez en el futuro podría añadir elementos que representen “aprobación” o “rechazo” del público de manera más simbólica.

3. Potencial generativo e interactivo
Sí, creo sinceramente que el algoritmo tiene mucho potencial generativo e interactivo. Me emociona pensar que la combinación de inputs puede generar variaciones infinitas en cada presentación: a veces la energía se manifiesta con muchas estrellas, otras con un fondo vibrante, y eso mantiene la experiencia viva y no repetitiva.
El uso de noise() y picos de entrada le da una cualidad orgánica que responde bien a la idea de una experiencia en tiempo real. Además, simular la interacción con sliders y botones en p5.js permite hacer pruebas efectivas antes de tener hardware real.

4. Viabilidad técnica (Preliminar)
En general, me siento capaz de implementar la mayoría del diseño usando p5.js, especialmente ahora que ya tengo un plan de simulación. Ya tengo experiencia con noise(), random() y clases en p5.js para crear partículas, así que no lo veo como un problema.
El mayor desafío técnico podría estar en la transición a inputs reales (si en el futuro se conectan sensores físicos o se usa WebSockets). Integrar datos en tiempo real desde un micro:bit o sensor de fuerza podría requerir práctica extra, especialmente en la sincronización y manejo de errores.

5. Fortalezas y debilidades
La mayor fortaleza de mi diseño es su expresividad visual y la forma en que combina inputs para generar emociones. El uso del storytelling en tiempo real, con estrellas como metáfora de energía, me parece poético e innovador.
La debilidad más notoria es que puede volverse visualmente caótico si no calibro bien los umbrales y las cantidades de partículas. También debo cuidar que los efectos no se saturen visualmente al combinar entradas altas. Esto requerirá muchos ajustes finos en la implementación para mantener la experiencia armónica y no abrumadora.
