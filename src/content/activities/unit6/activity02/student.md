#### Actividad 2

Inputs: tabla o lista detallada (Fuente, Tipo, Rango/Formato, Simulación?, Conexión Storytelling).

|Fuente|Tipo de dato|Rango/Formato|Simulación?|Conexion con el storytelling|
|------|------------|-------------|-----------|----------------------------|
| Sensores de presión en la pasarela | Numérico| 0.0 a 1 (intensidad)| Voy a simularlo, no se si hacerlo con Unity o que herramienta pero mi experiencia requiere una simulación de todos los resultados, me parece que para que se entienda la escencia es necesario que haya una modelo| Cada paso de las modelos generan las mini galaxias y nebulosas en la pasarela|
| Micrófonos ambientales | Número | 0 - 100 db | Esto lo parametrizaria directamente, pondria unos valores iniciales para simular todo, porque es muy engorroso poner un tipo de audio digital | Los aplausos y gritos de los usuarios desencadenan mini explosiones en los pasos de las modelos y en el domo |
| Aplicación interactiva (votación de los fondos) | Texto (botones) | Fondo x temática | La simulacion seria la proyeccion en el domo | Los asistentes eligen en tiempo real la atmosfera del domo, influyendo en la narrativa visual que encapsula lo que el usuario interpreta de cada prenda|
| Control remoto (tablet o pc) | Número| 0-10 (ajuste)| Seria simplemente unas barras de controles para que no quede muy pesada visualmente la experiencia | El equipo de produccion (o yo) modifica la intensidad de los efectos visuales en tiempo real|


Process: descripción textual detallada. Incluye pseudocódigo o un diagrama de flujo si te ayuda a clarificar la lógica. Explica la generatividad, respuesta en tiempo real y conexión al Storytelling.

1. Los sensores de presión en la pasarela registran la intensidad de los pasos. Si la intensidad supera un umbral, se activa la generación de una nueva galaxia.

2. Los micrófonos detectan el nivel de ruido del público. Si el nivel supera cierto límite, se generan explosiones de luz en el domo.

3. La aplicación recopila las votaciones en tiempo real y cambia el fondo del escenario según la opción más votada.

4. El equipo de producción ajusta la intensidad de los efectos visuales a través del control remoto según la atmósfera deseada.

Pseudocódigo: 
```c
SI (presion_pasarela > umbral) ENTONCES
    generar_galaxia();

SI (nivel_sonido > limite) ENTONCES
    activar_explosion_luz();

fondo_actual = obtener_votacion_mas_alta();
actualizar_fondo_escenario(fondo_actual);

SI (usuario_escanea_vestido) ENTONCES
    mostrar_info_RA();

ajustar_efectos_visuales(control_remoto);
```
Conexión con el Storytelling:

Cada acción de los asistentes y modelos influye en la evolución del "universo digital" del desfile.

Los pasos representan la formación de galaxias, mientras que el público es quien altera el cosmos.

Outputs: descripción detallada (Tipo, Elementos, Propiedades Dinámicas). Explica la relación Input->Process->Output y cómo manifiestan el Storytelling. Puedes incluir bocetos simples si es visual.

| Tipo | Elementos | Propiedades Dinámicas | ¿Como manifiestan el storytelling?|
|------|-----------|-----------------------|-----------------------------------|
|Visual| Galxias en pasarela | Posicion, tamaño y brillo| Expansión del universo con cada paso|
|Visual| Explosiones de luces en el domo| Color, intensidad y duracion|Representa la energía del publico y su efecto como fuerza gravitacional|
|Visual| Fondo del escenario (domo)| Imagenes con transición suave| Se adapta a la atmósfera deseada por el publico destacando su control en nuestro universo|
|Estadistico|Datos en tablet| Numeros y data en vivo| Muestra el impacto del público en la experiencia|

