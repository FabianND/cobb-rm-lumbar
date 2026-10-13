# Ficha de lectura · Niglas *et al.* 2026

**Cita:** Niglas M, Whitcher B, Amiras D, Thanaj M, Basty N, Bell-Bradford C, Thomas EL, Bell JD. Detecting scoliosis at scale using automated Cobb angle analysis in the UK Biobank. *Eur Spine J.* 2026 (publicado en línea 17-ago-2026). doi:[10.1007/s00586-026-10239-1](https://doi.org/10.1007/s00586-026-10239-1). PMID 42606698. 


**Fecha de lectura:** 5-oct-2026 · **Leído completo:** sí



|Campo|Lo que dice el artículo|Pág./sección|
|-|-|-|
|Pregunta / objetivo|Desarrollar un método automático para estimar el ángulo de Cobb a partir de RM Dixon y aplicarlo a la cohorte UK Biobank para caracterizar la presencia y magnitud de la curvatura espinal en población general. Además, exploran asociaciones entre la curvatura y variables antropométricas, composición corporal y dolor. Los autores plantean el método principalmente como una herramienta de fenotipado epidemiológico a gran escala, no como una herramienta diagnóstica clínica.|Abstract; Introduction|
|Diseño|Estudio observacional transversal realizado sobre participantes del UK Biobank con RM abdominal Dixon disponible. El estudio cuenta con aprobación ética del North West Multi-centre Research Ethics Committee (11/NW/0382), consentimiento informado y autorización del UK Biobank (application 44584).|Methods: Data|
|Población (edad, sexo, n)|33.889 participantes incluidos en el análisis final. Edad media: 63,9 ± 7,7 años; 49,9 % mujeres; aproximadamente 97 % blancos. El UK Biobank reclutó participantes de 40–85 años. Se excluyeron participantes con datos faltantes y aquellos con escoliosis juvenil o diagnóstico de escoliosis antes de los 18 años. Hay una pequeña discrepancia en el número inicial de participantes con Dixon entre secciones del artículo: 40.769 en Study design frente a 40.755 en Results.|Study design; Results; Table 1|
|Modalidad, secuencia, posición|RM Dixon de cuello a rodilla, adquirida como parte del protocolo de imagen abdominal del UK Biobank. El análisis utiliza la representación de médula ósea vertebral obtenida mediante la técnica Dixon. La adquisición se realizó en decúbito supino. Se analizaron 18 compartimentos vertebrales desde T1 hasta S1. El ángulo se calcula en el plano coronal mediante las coordenadas x-z. La resolución espacial y grosor de corte no están especificados en el texto principal y se remiten a referencias previas del protocolo de adquisición.|Image processing|
|Segmentación|Una red neuronal segmentó automáticamente los compartimentos de médula ósea vertebral (VBM) desde T1 hasta S1. Para entrenarla se utilizaron 120 participantes anotados manualmente, divididos 80/20 entre entrenamiento y prueba. El modelo obtuvo un Dice de 0,83 en el conjunto de prueba. La arquitectura concreta de la red no se describe en detalle en el texto principal.|Image processing|
|Cálculo del ángulo|Se calculan los centroides de los compartimentos VBM y se ajusta un spline cúbico utilizando sus coordenadas en el plano coronal. A partir de la segunda derivada del spline se identifican los puntos de inflexión que delimitan las curvas. El ángulo se calcula entre las perpendiculares al spline en puntos de inflexión adyacentes y entre las vértebras terminales y sus puntos de inflexión más cercanos. Se utiliza como fenotipo el máximo ángulo obtenido para cada participante. Por tanto, es una aproximación al Cobb convencional basada en la trayectoria de los centroides de la médula ósea, no en los platillos vertebrales.|Image processing; Fig. 1; Discussion|
|Referencia (ground truth) y validación del método|La referencia manual fue obtenida por un único radiólogo con 21 años de experiencia, coautor del estudio. Midió el Cobb en 35 participantes, seleccionados para representar diferentes sexos y niveles de severidad, y repitió las mediciones después de 11–30 días. El artículo no especifica claramente en el texto qué modalidad/imagen exacta utilizó el radiólogo para la medición manual. La concordancia se evaluó mediante Bland–Altman y métricas de correlación/error.|Quality control; Results; Fig. 7|
|Error manual vs. automático|En la comparación manual–automática, el sesgo fue +6,73°, indicando una tendencia del método automático a producir ángulos mayores que la medición manual. La figura reporta MAE 8,88°, RMSE 10,87° y r = 0,83. Los límites de acuerdo de la figura son aproximadamente −10,25° a +23,71°; el texto los resume como aproximadamente ±17°. El sesgo fue especialmente evidente en los ángulos bajos y medios, lo que puede afectar la clasificación alrededor del umbral de 10°.|Results; Fig. 7|
|Variabilidad del observador|La repetición de las mediciones manuales por el mismo radiólogo produjo un sesgo de −0,80°, MAE de 4,61°, r = 0,89 y límites de acuerdo aproximadamente de −13,47° a +11,86°. Esto demuestra que incluso la medición manual presenta una variabilidad considerable.|Results; Fig. 7|
|Control de calidad|Se realizó revisión visual en tres grupos de 50 participantes: aquellos con Cobb más alto, más bajo y una muestra aleatoria. Se identificaron y corrigieron 115 etiquetas vertebrales erróneas, principalmente etiquetas espurias alrededor de hombros y caderas que podían alterar el spline y producir Cobb artificialmente elevados. También se revisaron 49 participantes con diagnóstico clínico de escoliosis pero Cobb automático <10°, confirmándose visualmente la segmentación.|Quality control|
|Umbral y definición de escoliosis|Se definió escoliosis mediante Cobb máximo >10°, siguiendo SOSORT 2016. Severidad: 0–9° = ninguna; 10–24° = leve; 25–39° = moderada; ≥40° = grave. Los autores mantienen el umbral de 10° aunque reconocen que la medición en supino puede producir ángulos 7–12° menores que una radiografía de pie.|Scoliosis and pain definitions; Introduction|
|Resultados principales|El Cobb medio fue 8,72 ± 5,21°, con rango de 0,9–86,6°. 9.497 participantes (28 %) tuvieron Cobb >10°. La mayoría de los positivos fueron leves: aproximadamente 27 % de toda la cohorte presentó curvatura leve, 1,2 % moderada y 0,3 % grave. Solo 170 participantes (0,5 %) tenían diagnóstico registrado de escoliosis. Entre los diagnosticados, 121 también fueron positivos por el algoritmo y 49 no superaron los 10°. Entre los no diagnosticados, 9.376 fueron positivos por el algoritmo.|Results; Table 1; Fig. 3|
|Interpretación del 28 %|El 28 % debe interpretarse como la proporción de participantes que superó el umbral de 10° según el método automático, no como una prevalencia clínica confirmada de escoliosis. Esta distinción es especialmente importante porque el método presentó un sesgo positivo de 6,73° frente a la medición manual, particularmente en ángulos bajos y medios, precisamente alrededor del umbral utilizado para clasificar escoliosis. Los propios autores reconocen que este sesgo puede contribuir a la elevada proporción de casos leves.|Results; Discussion|
|Asociaciones reportadas|En los modelos ajustados, la edad mostró la asociación más fuerte. También se observaron asociaciones con PDFF paraespinal, dolor lumbar crónico y talla; VAT presentó asociación negativa. El volumen del iliopsoas mostró asociación negativa y la osteoporosis positiva únicamente en hombres. Sin embargo, las correlaciones de Spearman fueron débiles (todas r <0,25) y los modelos explicaron poca variabilidad (R² = 0,085 en mujeres y 0,065 en hombres). Las diferencias de Cobb entre grupos de dolor fueron menores de 2°.|Results; Fig. 5–6; Tables 2–4|
|Limitaciones declaradas|La adquisición en supino puede reducir el Cobb respecto a una medición de pie y afectar la clasificación con umbral de 10°. La densidad mineral ósea solo se incorporó indirectamente. La baja prevalencia de enfermedad degenerativa codificada limita el análisis de esta condición. Los modelos explican menos del 10 % de la variabilidad. Además, resulta difícil distinguir entre escoliosis de aparición en la edad adulta y escoliosis adolescente residual. Los autores también reconocen que el sesgo del método en ángulos bajos puede contribuir a la elevada cantidad de casos clasificados como leves.|Discussion|
|Limitaciones que yo veo (**inferencia propia**)|1. Validación manual limitada: solo participaron 35 casos y hubo un único lector, que además era coautor.<br />2. Selección de los 35 casos: fueron seleccionados para representar sexo y severidad, por lo que no constituyen una muestra aleatoria y pueden no reflejar el desempeño poblacional real. <br />3. Validación concentrada en una sola persona: no permite estimar adecuadamente la variabilidad interobservador. <br />4. Constructo diferente: el método automático calcula la curvatura de un spline basado en centroides de médula ósea, mientras que el Cobb convencional se basa en la orientación de los platillos vertebrales; por tanto, no son exactamente la misma medida anatómica. <br />5. Problema alrededor de 10°: el sesgo positivo de +6,73° es particularmente relevante porque el umbral de clasificación es 10°. <br />6. Posible influencia de errores de segmentación: las 115 correcciones muestran que errores en las etiquetas pueden modificar considerablemente el spline. <br />7. Generalización: la cohorte es predominantemente blanca (97 %), lo que limita la generalización a otras poblaciones. <br />8. Imagen en supino: además de ser una limitación declarada, hace que la comparación con el Cobb radiográfico convencional no sea directamente equivalente. <br />9. La cifra del 28 % no debe utilizarse como prevalencia clínica confirmada. Es una prevalencia/proporción derivada del algoritmo y afectada por el error de medición y por las características de la población.|Inferencia propia a partir del artículo|
|Código y datos disponibles|Los datos originales del UK Biobank no son de acceso público directo. Pueden solicitarse mediante el procedimiento de acceso del UK Biobank a investigadores que cumplan sus requisitos. El artículo no proporciona una declaración de disponibilidad de código fuente del método automático, por lo que la reproducción independiente del pipeline completo no es posible únicamente con el material publicado.|Data availability|
|Qué aporta a mi proyecto|Es un antecedente muy relevante porque demuestra que es posible realizar detección/medición automática de curvatura espinal a gran escala mediante RM, incluso a partir de una adquisición Dixon que no fue diseñada específicamente para medir Cobb. Para nuestro proyecto, refuerza la importancia de separar segmentación, estimación de la curvatura y validación contra medición humana. También muestra que no basta con obtener una buena correlación: hay que analizar MAE, RMSE, sesgo y límites de acuerdo, especialmente alrededor del umbral clínico. Además, su sesgo en ángulos bajos justifica analizar específicamente la zona cercana a 10° y no limitarse al rendimiento global.|Aplicación al proyecto|



**Pregunta clave a responder al leer:** ¿Cómo validaron que el ángulo basado en centroides se aproxima al Cobb humano y con qué error?



Lo validaron comparando el método automático con mediciones manuales realizadas por un único radiólogo con 21 años de experiencia, en 35 participantes seleccionados para cubrir diferentes sexos y severidades. El mismo radiólogo repitió las mediciones manuales 11–30 días después para estimar su propia variabilidad. La comparación se realizó mediante Bland–Altman y otras métricas de error.



Para manual vs. automático, encontraron un Sesgo: +6.73°, MAE: 8.88°, RMSE: 10.87°, Correlación: r = 0.83, límites de acuerdo de la figura: −10.25° a +23.71° y el error/sesgo fue mayor en ángulos bajos y medios.



En cambio, para manual vs. repetición manual, encontraron un Sesgo: −0.80°, MAE: 4.61°, r = 0.89 y límites de acuerdo aproximadamente −13,47° a +11,86°



El 28 % representa la proporción de participantes que superó los 10° según el método automático y no debe interpretarse directamente como prevalencia clínica confirmada de escoliosis, especialmente debido al sesgo positivo observado en ángulos bajos y medios.



























