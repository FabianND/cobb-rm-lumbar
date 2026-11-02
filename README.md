# Cobb coronal en RM lumbar sagital: reproducción abierta y evaluación de robustez
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23410108.svg)](https://doi.org/10.5281/zenodo.23410108)

> **Solo investigación. No es un dispositivo médico ni está destinado al diagnóstico.** Los resultados de este repositorio no deben utilizarse para tomar decisiones sobre pacientes.

*English summary below.*

## Pregunta

¿Es posible reproducir de forma independiente y abierta un método automático para estimar la curvatura coronal de la columna a partir de RM lumbar sagital de rutina en adultos? ¿Qué tan estables son sus resultados ante cambios en el grosor de corte, la secuencia de adquisición (T1/T2) y las características técnicas de los estudios?

## Alcance

El proyecto se encuentra en su **etapa 1, dedicada a la validación técnica con datos públicos**. Utiliza SPIDER y, desde la cuarta semana, dos conjuntos externos: RSNA LumbarDISC y Lumbar Spine MRI Dataset de Mendeley. No utiliza datos de pacientes procedentes de instituciones vinculadas al proyecto. La población objetivo son adultos, pero los datos públicos no permiten comprobarlo en todos los casos ya que SPIDER solo informa la edad de 41 de sus 218 pacientes y RSNA no conserva la edad.
 
El trabajo parte de la reproducción y el examen del código publicado por van der Graaf *et al.* (2024). Se conserva la versión exacta del código utilizado, identificada mediante su commit y su huella digital, y se documentan las decisiones metodológicas, las adaptaciones necesarias y los resultados de cada etapa. También se estudia cuánto cambia la medición ante distintas condiciones técnicas de adquisición y segmentación.
 
El proyecto **no diagnostica escoliosis, no predice su aparición ni su progresión y no reemplaza la radiografía de columna en bipedestación**. Para evitar confusiones, el resultado se denomina *ángulo coronal lumbar estimado en RM sagital*. Aunque el procedimiento se basa en el método de Cobb, esta medición se obtiene con el paciente en decúbito y a partir de imágenes sagitales, por lo que no equivale al Cobb radiográfico en bipedestación.

## Estado

| Semana | Entregable | Estado |
|---|---|---|
| 1 | Inventario de SPIDER y ejecución verificada de `compute-Cobb-angle.py` (cuadernos 01 y 02) | Completado |
| 1 | Protocolo de la revisión de alcance registrado en OSF (`docs/revision_alcance/`) | Completado |
| 1 | Preguntas a los autores del script y del conjunto de datos ([DIAGNijmegen/cobb-angle-algorithm#1](https://github.com/DIAGNijmegen/cobb-angle-algorithm/issues/1); seguimiento en [FabianND/cobb-rm-lumbar#1](https://github.com/FabianND/cobb-rm-lumbar/issues/1)) | Respondido |
| 2 | Evaluación del disco más caudal y robustez frente al grosor de corte (cuadernos 03 y 04) | Completado |
| 3 | Comparación de segmentación automática frente a manual y medición sobre platillos vertebrales (cuadernos 05 y 06) | Completado |
| 4 | Cierre de las preguntas de los cuadernos 01 a 06 y definición de la regla de emparejamiento del artículo (cuaderno 07) | Completado |
| 4 | Incorporación de RSNA LumbarDISC y Mendeley, inventario, segmentación con TotalSpineSeg y revisión técnica sin calcular ángulos (cuadernos 08 y 09; segmentación en `notebooks/kaggle/`) | Completado |
| 4 | Plan de análisis del cuaderno 10 registrado en OSF ([doi:10.17605/OSF.IO/KP5DU](https://doi.org/10.17605/OSF.IO/KP5DU)) | Completado |
| 5 | Cálculo del ángulo coronal en RSNA y Mendeley según el plan registrado (`notebooks/10_angulo_coronal_externo.ipynb`) | Completado |
| 5 | Exploración de los resultados del cuaderno 10 (`notebooks/11_exploracion_angulo_coronal.ipynb`) | Completado |

## Semanas 1 a 4: reproducción del método y preparación de los datos externos
 
Las primeras cuatro semanas se dedicaron a reproducir el método publicado, examinar sus decisiones geométricas y preparar dos conjuntos externos para evaluar su comportamiento.
 
Con SPIDER, que contiene 218 pacientes y 447 series con máscaras manuales, se verificó el inventario frente al artículo publicado en *Scientific Data*. Después se ejecutó `compute-Cobb-angle.py` con las versiones del script, de la dependencia Tiger y de las máscaras fijadas y comprobadas mediante sus huellas digitales (cuadernos 01 y 02).
 
Los cuadernos 03 y 04 estudiaron la influencia de la cara inferior del disco más caudal y del grosor de corte. La cara inferior del disco 201 forma parte del par que define el ángulo en 141 de las 340 máscaras únicas (41,5 %). Por otra parte, el experimento controlado de remuestreo mostró que aumentar el grosor de corte reduce el ángulo una mediana de 0,22° a 3,3 mm y de 0,40° a 4,4 mm. El efecto fue pequeño y aproximadamente proporcional al ángulo inicial.
 
En la tercera semana se compararon dos segmentadores automáticos, SPIDER-Baseline-IIS y TotalSpineSeg, con las máscaras manuales de SPIDER. TotalSpineSeg presentó límites de acuerdo de aproximadamente ±2,2° y un sesgo medio cercano a cero. SPIDER-Baseline-IIS mostró un acuerdo estrecho en la mayoría de los casos adecuados, pero también fallos graves aislados, como el de la serie 167_t1, en la que produjo 73,2° frente a 7,1° con la máscara manual. El cuaderno 06 exploró una medición alternativa sobre los platillos vertebrales, con resultados próximos a los obtenidos mediante las caras de disco.
 
El cuaderno 07 resolvió una discrepancia entre el script y la regla de emparejamiento descrita en el artículo. El problema se debía a la convención de numeración: SPIDER numera los discos de abajo hacia arriba, mientras que el algoritmo se desarrolló con etiquetas ordenadas de arriba hacia abajo. Al ejecutar el script sin adaptar esa convención, el ángulo se sobreestima 0,39° en promedio frente a la regla del artículo. A partir de ese análisis, el proyecto adoptó el emparejamiento descrito por los autores como referencia.
 
El mismo cuaderno comparó distintas fórmulas para estimar la inclinación coronal de cada cara de disco. Se adoptó como fórmula principal una propuesta basada en el eje lateral proyectado,
 
$$
\arctan\left(\frac{n_x n_z}{1-n_x^2}\right),
$$
 
mientras que la fórmula del método publicado,
 
$$
\arctan\left(\frac{n_x}{n_z}\right),
$$
 
se conserva para comparación. La fórmula del eje lateral es una propuesta metodológica de este proyecto y todavía no ha sido validada frente a mediciones clínicas.
 
En la cuarta semana se incorporaron RSNA LumbarDISC y Lumbar Spine MRI Dataset de Mendeley. El cuaderno 08 realizó el inventario, la conversión de las imágenes a NIfTI y la selección de una serie T1 y otra T2 por estudio. El cuaderno 09 segmentó las imágenes con TotalSpineSeg y revisó las máscaras sin calcular todavía ningún ángulo. Entre el 89,9 % y el 95,3 % de las máscaras cumplieron los criterios técnicos de utilización. La comparación de las medidas disponibles no mostró una ventaja suficientemente clara de T2, por lo que T1 se estableció como secuencia principal mediante una regla definida antes de comparar las secuencias.
 
El plan de análisis del cuaderno 10 se registró en OSF el 31 de octubre de 2026, antes de calcular los ángulos en los dos conjuntos externos.
 
### Respuesta de los autores del método original
 
Jasper van der Graaf, autor del método, respondió las preguntas planteadas en el issue del repositorio original. Confirmó que el código publicado corresponde al utilizado en el artículo, explicó que las máscaras idénticas entre T1 y T2 de SPIDER se deben a que se seleccionaba la mejor segmentación corregida y se reutilizaba para ambas secuencias cuando correspondía, y aclaró que la numeración de arriba hacia abajo explica la regla de emparejamiento implementada en el script.
 
Para consultar los detalles de las primeras cuatro semanas, las figuras y los resultados completos, puede revisarse el README de la versión [v0.0.4](https://github.com/FabianND/cobb-rm-lumbar/blob/v0.0.4/README.md), junto con su [release](https://github.com/FabianND/cobb-rm-lumbar/releases/tag/v0.0.4) (doi:[10.5281/zenodo.23848342](https://doi.org/10.5281/zenodo.23848342)). Las versiones anteriores se encuentran en la sección de releases del repositorio.
 
## Semana 5: evaluación del ángulo en los conjuntos externos
 
### Cuaderno 10: análisis preregistrado
 
El cuaderno 10 ejecutó el plan de análisis registrado en OSF. Antes de procesar los conjuntos externos, se realizó un control positivo para comprobar que la versión optimizada del script, que procesa cada disco dentro de su propia caja, reprodujera los planos obtenidos en los cuadernos 03 y 05 para las 894 máscaras de SPIDER. Los reprodujo exactamente, con una diferencia de 0,0° en todas las caras.
 
Con esa versión se calcularon los planos y centroides de las 4.971 series seleccionadas que tenían máscara, sin ningún error. Las otras seis de las 4.977 no fallaron en este cálculo, sino que llegaron sin máscara desde la segmentación del cuaderno 09: TotalSpineSeg no produjo máscara para cinco series T2 de Mendeley, y una T1 de RSNA no se pudo convertir a NIfTI, así que nunca llegó a segmentarse. Entraron al análisis como datos faltantes, según se decidió antes de calcular los ángulos.
 
La comparación entre T1 y T2 del mismo estudio mostró un acuerdo alto. En Mendeley, los límites de acuerdo fueron de −1,65° a 1,63° para 510 estudios, con un ICC(A,1) de 0,956. En RSNA, los límites fueron de −2,08° a 1,89° para 1.971 estudios, con un ICC(A,1) de 0,978. El sesgo fue cercano a cero en ambos conjuntos.
 
Estas cifras deben interpretarse como una estimación optimista de la variabilidad entre secuencias. T1 y T2 comparten paciente, sesión y segmentador, por lo que la comparación no recoge todas las fuentes de error que aparecerían al repetir el procedimiento en adquisiciones y segmentaciones independientes.
 
La hipótesis preregistrada H1 se cumplió en ambos conjuntos: con la fórmula del eje lateral proyectado, los límites de acuerdo fueron 0,18° más estrechos en Mendeley y 0,33° más estrechos en RSNA que con la fórmula del método publicado. Sin embargo, un análisis exploratorio posterior mostró que esta ventaja se debe principalmente a que la fórmula del eje lateral produce ángulos entre un 3 % y un 5 % menores. Una vez descontada esa diferencia de escala, la precisión relativa de ambas fórmulas resulta muy similar.
 
El error estimado por cara fue de aproximadamente 0,5°. Con ese error, una columna recta simulada de seis a ocho discos daría por azar un ángulo de hasta unos 2° (percentil 95), muy por debajo del umbral de 10° usado en el análisis. Ese umbral se toma del Cobb radiográfico y no puede trasladarse directamente a la medición en RM.
 
En las series T1, el 4,1 % de los estudios de Mendeley y el 15,1 % de los de RSNA alcanzaron un ángulo de 10° o más. Estos porcentajes no representan prevalencias de escoliosis. La medición se obtiene en decúbito a partir de RM sagital y los dos conjuntos corresponden a pacientes remitidos a una resonancia lumbar, no a muestras poblacionales evaluadas con radiografías de pie.
 
En Mendeley, cuatro de los cinco pacientes cuyos informes mencionan escoliosis se situaron entre los cuatro ángulos más altos de los 515 estudios, con un AUC descriptivo de 0,971. Este resultado debe interpretarse con cautela: se basa en solo cinco informes, dos de ellos posiblemente asociados de forma incorrecta a su carpeta, y el analista conocía esa información antes de calcular los ángulos. Por tanto, no constituye una evaluación de exactitud diagnóstica.
 
El cuaderno también comparó el estimador basado en centroides vertebrales con el basado en las caras de disco. El primero fue considerablemente menos repetible, con límites de acuerdo de 8,7° y 9,3° de ancho en los dos conjuntos. Un análisis exploratorio en RSNA mostró además que la ventaja aparente de T2 al coincidir con los niveles anatómicos marcados dependía principalmente del tipo de punto de referencia utilizado, y no de una diferencia demostrada en la calidad de la segmentación.
 
### Cuaderno 11: análisis exploratorio
 
El cuaderno 11 trabajó sobre los planos, centroides y tablas que dejó el cuaderno 10, sin volver a ejecutar el script ni el segmentador. Su objetivo fue examinar cuatro preguntas que surgieron al revisar los resultados del análisis principal.
 
Primero, se revisaron visualmente las 20 series de Mendeley con mayor ángulo cuyos informes no mencionaban escoliosis. Doce se clasificaron como curvas con segmentación correcta, tres presentaron errores de segmentación y cinco se consideraron dudosas. Cuatro de estas últimas tenían estructuras vertebrales o discos situados en el borde del campo de visión. Esto muestra que la ausencia de una mención de escoliosis en un informe no equivale a demostrar que la columna sea recta. La revisión fue realizada por un solo evaluador, sin cegamiento ni una segunda lectura independiente.
 
Segundo, se repitió el análisis utilizando únicamente los discos lumbares. La proporción de estudios con ángulos de 10° o más disminuyó del 4,1 % al 3,5 % en Mendeley y del 15,1 % al 12,3 % en RSNA. La diferencia entre los conjuntos se mantuvo, por lo que los discos torácicos que entran en el campo de visión no explican por sí solos la diferencia observada. La restricción a los discos lumbares también mejoró ligeramente la repetibilidad, con límites de acuerdo de 2,85° y 3,32° de ancho, frente a 3,25° y 3,94° con todos los discos sobre los mismos estudios.
 
Tercero, se examinó la relación entre las marcas de calidad de las máscaras y los ángulos elevados. En Mendeley, las marcas de máscara no utilizable y de disco en el borde del campo aparecieron con mayor frecuencia entre los ángulos grandes. En RSNA, la relación con la marca de disco en el borde fue mucho menos evidente. Estas marcas no deben utilizarse como criterios automáticos de exclusión sin una evaluación adicional, porque podrían eliminar de forma desproporcionada casos con curvaturas mayores o con una cobertura anatómica particular.
 
Por último, se evaluó un *spline* cúbico suavizado como alternativa para estimar la orientación a partir de los centroides vertebrales. El método empeoró la repetibilidad respecto al estimador original por centroides y no ofreció una ventaja que justificara conservarlo.
 
Estos análisis son exploratorios. No modifican el plan registrado del cuaderno 10 ni sus resultados principales. Cualquier cambio metodológico que surja de ellos deberá registrarse antes de evaluarse en nuevos análisis.
 
## Interpretación y limitaciones
 
Los resultados de las cinco primeras semanas describen la reproducción del método, su comportamiento ante variaciones técnicas y su repetibilidad en dos conjuntos externos. **No demuestran la exactitud clínica de la medición ni su capacidad para diagnosticar escoliosis.**
 
Ninguno de los conjuntos utilizados proporciona un ángulo de Cobb de referencia medido por especialistas sobre radiografías en bipedestación. Por tanto, no es posible establecer cuánto se aproxima el resultado del algoritmo a una medición clínica de referencia.
 
También existen limitaciones relacionadas con los propios datos. RSNA no conserva en las cabeceras disponibles la institución, el fabricante y modelo del escáner, el campo magnético, el sexo ni la edad de los pacientes. Aunque el conjunto original procede de varias instituciones, no es posible asignar cada estudio a su centro de origen. Mendeley, por su parte, procede de un único escáner. Además, aunque la población objetivo son adultos, no puede comprobarse que todos los estudios analizados lo sean, porque SPIDER solo informa la edad de 41 de 218 pacientes y RSNA no conserva la edad. En consecuencia, el proyecto puede estudiar diferencias entre conjuntos y características técnicas recuperables, pero no estimar directamente el efecto de distintos hospitales o equipos.
 
La repetibilidad entre T1 y T2 tampoco equivale a reproducibilidad entre adquisiciones independientes, porque ambas secuencias pertenecen al mismo estudio y se procesan con el mismo segmentador. Además, los resultados dependen de la cobertura anatómica de las máscaras, de la selección del par de discos y de la calidad de la segmentación.
 
El siguiente paso necesario para avanzar hacia una validación clínica es disponer de mediciones de referencia realizadas por especialistas y asociadas a las imágenes correspondientes. Esa comparación permitirá estudiar la concordancia con el Cobb radiográfico y determinar qué utilidad, si alguna, puede tener la medición obtenida en RM.
 
Los detalles metodológicos, las figuras y la interpretación de cada experimento están disponibles en los cuadernos de `notebooks/`. Las tablas y los resultados se conservan en `salidas/`.
 
## Revisión de alcance: línea paralela de la etapa 1
 
El protocolo de revisión de alcance se registró en OSF el 12 de octubre de 2026 con el título *Automated and semi-automated measurement of coronal spinal curvature and detection of scoliosis on MRI and CT in adults: a scoping review protocol*.
 
- DOI: [10.17605/OSF.IO/WXQ5G](https://doi.org/10.17605/OSF.IO/WXQ5G)
- Proyecto: [osf.io/5pm9q](https://osf.io/5pm9q)
- Pregunta, criterios PCC y búsqueda de registros existentes: `docs/revision_alcance/`.
## Preregistro del análisis del cuaderno 10
 
Antes de calcular cualquier ángulo en RSNA o Mendeley, el 31 de octubre de 2026 se registró públicamente en OSF el plan de análisis del cuaderno 10, titulado *Measurement properties of an automated lumbar coronal angle estimated on routine sagittal MRI in two external datasets (RSNA LumbarDISC and Mendeley Lumbar Spine MRI): preregistered analysis plan*.
 
- DOI: [10.17605/OSF.IO/KP5DU](https://doi.org/10.17605/OSF.IO/KP5DU)
- Copia del plan: `salidas/resultados_semana4/09_segmentacion_externa/plan_analisis_cuaderno_10.md`
- SHA-256: `14548723494df98ce3fa0e78135a7c7dbe1317e985dadbdee97943f3e35f970b`
El cuaderno 10 verifica esta huella antes de comenzar el análisis. El plan se ejecutó sin desviaciones. Las aclaraciones y los análisis agregados después de conocer los resultados se identificaron por separado como exploratorios, al igual que los análisis del cuaderno 11.
 
El estudio evalúa propiedades de medición, no exactitud diagnóstica. Los resultados y las tablas correspondientes se encuentran en `salidas/resultados_semana5/`.
 
## Cómo ejecutar
 
Los conjuntos de datos no están incluidos en este repositorio ni se descargan automáticamente desde los cuadernos. Antes de ejecutarlos, es necesario descargar los datos y guardarlos en Google Drive, respetando la estructura de carpetas indicada en la tabla «Antes de ejecutar» de cada cuaderno.
 
SPIDER se descarga desde Zenodo (DOI: [10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290), versión v4) y es necesario para todos los cuadernos.
 
Los cuadernos 08 a 11 requieren, además, los dos conjuntos externos:
 
- **RSNA LumbarDISC.** Se descarga mediante la API de Kaggle después de aceptar las reglas de la competición RSNA 2024 Lumbar Spine Degenerative Classification. Su uso está sujeto a las condiciones de la competición, que incluyen restricciones de uso comercial y de redistribución.
- **Lumbar Spine MRI Dataset de Mendeley.** Se descarga desde Mendeley Data, junto con las notas de los radiólogos asociadas a los estudios.
Cada cuaderno se abre en Google Colab y se ejecuta mediante **Entorno de ejecución → Reiniciar y ejecutar todo**. Antes de utilizar los archivos, los cuadernos verifican las sumas MD5 de los datos y las huellas SHA-256 del script, de los pesos de los segmentadores y, en el cuaderno 10, del plan de análisis registrado.
 
Los cuadernos deben ejecutarse en orden, porque los posteriores utilizan resultados de los anteriores:
 
- El cuaderno 07 reúne los resultados de los cuadernos 01 a 06.
- El cuaderno 09 utiliza la selección realizada en el 08 y las máscaras generadas en Kaggle.
- El cuaderno 10 utiliza las máscaras y tablas del 09, junto con los planos calculados en los cuadernos 03 y 05.
- El cuaderno 11 trabaja sobre las tablas del cuaderno 10, sin volver a ejecutar el script ni el segmentador.
Solo la segmentación automática requiere GPU y se ejecuta por separado del resto del análisis. En el cuaderno 05 se activa mediante `CORRER_SEGMENTACION = True` y tomó entre 1 y 13 minutos por serie, según el segmentador y las condiciones de ejecución.
 
Las series de RSNA y Mendeley se segmentan en Kaggle mediante los cuadernos de `notebooks/kaggle/`. En las pruebas realizadas con dos GPU T4, el procesamiento tomó alrededor de 25 segundos por serie en cada GPU.
 
El resto del análisis se ejecuta en Colab gratuito sin GPU. El procesamiento más largo fue el cálculo de planos y centroides del cuaderno 10, que tomó aproximadamente seis horas para 4.971 máscaras. En los demás cuadernos, los tiempos observados van desde unos minutos hasta aproximadamente tres horas, dependiendo de la etapa y de los recursos disponibles.
 
Los cuadernos guardan los resultados al finalizar cada etapa. Por ello, si una sesión se interrumpe, es posible continuar a partir de los archivos que ya se hayan guardado. Las máscaras automáticas no se incluyen en el repositorio porque pueden generarse de nuevo a partir de los datos originales y de los cuadernos correspondientes.
 
## Datos, código y trabajos de referencia
 
- **SPIDER:** van der Graaf JW *et al.* *Scientific Data*. 2024;11:264. DOI: [10.1038/s41597-024-03090-w](https://doi.org/10.1038/s41597-024-03090-w). Datos: [10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290). Licencia CC BY 4.0.
- **Método original:** van der Graaf JW *et al.* *European Radiology*. 2024;34(9):5748–5757. DOI: [10.1007/s00330-024-10616-8](https://doi.org/10.1007/s00330-024-10616-8). Código: [DIAGNijmegen/cobb-angle-algorithm](https://github.com/DIAGNijmegen/cobb-angle-algorithm), commit `72c712f`.
- **Aplicación poblacional:** Niglas M *et al.* *European Spine Journal*. 2026. DOI: [10.1007/s00586-026-10239-1](https://doi.org/10.1007/s00586-026-10239-1).
- **Segmentador SPIDER-Baseline-IIS:** [DIAGNijmegen/SPIDER-Baseline-IIS](https://github.com/DIAGNijmegen/SPIDER-Baseline-IIS), licencia Apache-2.0, commit `438049a`. Método: Lessmann N *et al.* *Medical Image Analysis*. 2019;53:142–155. DOI: [10.1016/j.media.2019.02.005](https://doi.org/10.1016/j.media.2019.02.005).
- **Segmentador TotalSpineSeg:** [neuropoly/totalspineseg](https://github.com/neuropoly/totalspineseg), licencia LGPL-3.0, versión `20260807` y pesos `r20260730`. Basado en nnU-Net: Isensee F *et al.* *Nature Methods*. 2021;18:203–211.
- **Método de Cobb:** Cobb JR. *Outline for the study of scoliosis*. *Instructional Course Lectures*. 1948;5:261–275.
- **RSNA LumbarDISC:** competición [RSNA 2024 Lumbar Spine Degenerative Classification](https://www.kaggle.com/competitions/rsna-2024-lumbar-spine-degenerative-classification) en Kaggle. Descripción del conjunto: [arXiv:2506.09162](https://arxiv.org/abs/2506.09162). Su uso está sujeto a las condiciones de la competición; el repositorio conserva únicamente resultados agregados.
- **Lumbar Spine MRI Dataset:** Sudirman S *et al.* Mendeley Data, versión 2. DOI: [10.17632/k57fr854j2.2](https://doi.org/10.17632/k57fr854j2.2). Notas de los radiólogos: [10.17632/s6bgczr8s2.2](https://doi.org/10.17632/s6bgczr8s2.2), licencia CC BY 4.0.
- **Versiones exactas de los códigos y datos utilizados:** `docs/fuentes_externas.md`.
## Cómo citar
 
Nossa Díaz, E. F. (2026). *Cobb coronal en RM lumbar sagital: reproducción abierta y evaluación de robustez* [Software]. Zenodo. https://doi.org/10.5281/zenodo.23410108
 
El DOI anterior es el *concept DOI*, que identifica el proyecto en general y dirige a su versión más reciente. Cada versión publicada en Zenodo dispone también de un DOI propio. También puede utilizarse `CITATION.cff` o la opción *Cite this repository* de GitHub.
 
## Licencia
 
El código se distribuye bajo la licencia [Apache-2.0](LICENSE). Los datos de SPIDER y Mendeley conservan sus respectivas condiciones de uso y deben citarse de acuerdo con las indicaciones de sus autores.
 
En el caso de RSNA, el repositorio no contiene imágenes ni tablas individuales de los estudios. Se conservan únicamente resultados agregados, de acuerdo con las restricciones de la competición.
 
---
 
## English summary
 
Open and independent research reproduction of an automated method for estimating coronal lumbar curvature from routine sagittal MRI, based on van der Graaf *et al.* (2024, *European Radiology*). The project uses public datasets (SPIDER and, since week 4, RSNA LumbarDISC and the Mendeley Lumbar Spine MRI Dataset) to examine reproducibility and measurement behaviour across slice thickness, sequence (T1/T2), segmentation methods and external datasets. **Research only. Not a medical device and not for diagnosis.**
 
**Weeks 1–4:** The SPIDER inventory was verified against the *Scientific Data* article, and the published script was reproduced with pinned versions and checksum-verified files. The project examined the influence of the most caudal disc, slice thickness, automatic segmentation and vertebral endplate measurements. A label-order convention explained the mismatch between the original script and the article's pairing rule. The article's rule is now the reference, while the projected lateral-axis formula is used as the project's primary proposal; it has not been clinically validated. Two external datasets were then prepared and segmented. Between 89.9% and 95.3% of masks met the technical usability criteria, and T1 was selected as the primary sequence using a pre-specified rule. The analysis plan for notebook 10 was preregistered on OSF (doi: [10.17605/OSF.IO/KP5DU](https://doi.org/10.17605/OSF.IO/KP5DU)).
 
**Week 5:** Notebook 10 executed the preregistered analysis without deviations. T1–T2 agreement was high, with limits of agreement of −1.65° to 1.63° in Mendeley and −2.08° to 1.89° in RSNA, and ICC(A,1) values of 0.956 and 0.978, respectively. This agreement is an optimistic estimate because both sequences share the same patient, session and segmenter. Hypothesis H1 was met in both datasets, although a post hoc exploratory analysis showed that the narrower limits obtained with the projected lateral axis mainly reflect its smaller angle scale. In T1, 4.1% of Mendeley studies and 15.1% of RSNA studies reached 10° or more; these percentages are not scoliosis prevalence estimates.
 
Notebook 11 explored the results from the planes, centroids and tables of notebook 10, without rerunning the script or the segmenter. Visual review of the 20 highest-angle Mendeley series without a scoliosis mention in their reports classified 12 as curves with correct segmentation, three as segmentation errors and five as uncertain. Restricting the measurement to lumbar discs reduced the proportion of studies reaching 10° to 3.5% in Mendeley and 12.3% in RSNA, while slightly improving repeatability. Some quality flags were associated with higher angles in Mendeley, so they should not be used as automatic exclusion criteria without further evaluation. A smoothed cubic spline worsened the centroid-based estimator and was not retained.
 
None of the datasets provides an independently measured reference Cobb angle. Therefore, these results describe technical reproducibility and measurement behaviour, not clinical accuracy or diagnostic performance. Validation against specialist measurements, ideally with a radiographic standing Cobb reference, remains a necessary next step.
