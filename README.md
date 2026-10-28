# Cobb coronal en RM lumbar sagital: reproducción abierta y prueba de robustez
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23410108.svg)](https://doi.org/10.5281/zenodo.23410108)

> **Solo investigación. No es un dispositivo médico ni sirve para diagnóstico.** Nada en este repositorio debe usarse para tomar decisiones sobre pacientes.

*English summary below.*

## Pregunta

¿Se puede reproducir de forma independiente y abierta la medición automática del ángulo de Cobb coronal a partir de RM lumbar sagital de rutina en adultos, y qué tan estable es esa medición cuando cambian el grosor de corte, la secuencia (T1/T2) y el centro de adquisición?

## Alcance

Este proyecto está en su **etapa 1 (validación técnica con datos públicos)**. Trabaja sobre el dataset público SPIDER y no usa datos de pacientes de ninguna institución.

Lo que sí hace es ejecutar y examinar el código publicado por van der Graaf *et al.* (2024) en las condiciones exactas en que se descargó (commit y huella registrados), documentar cada decisión y medir la variabilidad del resultado ante cambios técnicos de la imagen.

Lo que no hace es diagnosticar escoliosis, predecir su aparición o progresión, ni reemplazar la radiografía de pie. El valor medido es un **"Cobb coronal en decúbito en RM"**, que no equivale al Cobb radiográfico en bipedestación.

## Estado

| Semana | Entregable | Estado |
|---|---|---|
| 1 | Inventario verificado de SPIDER (`notebooks/01_inventario_spider_drive.ipynb`) | Completado |
| 1 | Ejecución de `compute-Cobb-angle.py` sobre las 447 máscaras, con versiones fijadas y verificadas (`notebooks/02_compute_cobb_angle.ipynb`) | Completado |
| 1 | Celdas de inspección visual e interactiva del algoritmo (cuaderno 02) | Completado |
| 1 | Protocolo de la revisión de alcance registrado en OSF (`docs/revision_alcance/`) | Completado |
| 1 | Preguntas a los autores del script y del dataset ([DIAGNijmegen/cobb-angle-algorithm#1](https://github.com/DIAGNijmegen/cobb-angle-algorithm/issues/1); seguimiento en [#1](https://github.com/FabianND/cobb-rm-lumbar/issues/1)) | Respondido |
| 2 | El disco más caudal en las 447 series y tres variantes del cálculo (`notebooks/03_disco_caudal_y_variantes.ipynb`) | Completado |
| 2 | Robustez frente al grosor de corte (`notebooks/04_robustez_grosor_de_corte.ipynb`) | Completado |
| 3 | Ángulo con segmentación automática (SPIDER-Baseline-IIS y TotalSpineSeg) frente a la manual (`notebooks/05_segmentacion_automatica.ipynb`) | Completado |
| 3 | Ángulo medido en los platillos vertebrales frente a las caras de disco (`notebooks/06_cobb_por_platillos.ipynb`) | Completado |

## Trabajo realizado en la primera semana

### 1. Inventario de SPIDER antes de medir nada

El cuaderno 01 describe el dataset a partir de `overview.csv` y de las propias máscaras, después de verificar las sumas MD5 de los archivos contra la descarga de Zenodo. Los conteos principales coinciden con los del artículo de *Sci Data*: 218 pacientes, 447 series (196 T1, 210 T2 y 41 T2 SPACE), 3125 vértebras y 3147 discos; las mujeres son 136 (62,4 %; el artículo reporta 63 %); además, el número de vértebras y de discos de cada máscara coincide con el que declara `overview.csv` en las 447 series. El inventario dejó tres limitaciones que condicionan todo lo que sigue:

- **No hay columna de hospital.** El centro se aproximó con una inferencia: los estudios con T2 SPACE se asignan al centro universitario, como describe el artículo, y el resto se agrupa por escáner (8 combinaciones de fabricante, modelo y campo de 1,5 T o 3 T). Un grupo de escáner no equivale a un hospital.
- **La edad solo está disponible para 41 de 218 pacientes (19 %),** todos en el grupo asignado al centro universitario. Para los otros 177 no se puede comprobar que sean adultos, que es la población de este proyecto.
- **El grosor de corte de las series estándar va de 3 a más de 5 mm** (258 series de 3–4 mm, 144 de 4–5 mm y 4 de 5 mm o más), frente a menos de 1 mm en T2 SPACE. Esta variación es la base del análisis de robustez previsto.

### 2. Reproducción verificable del algoritmo publicado

El cuaderno 02 descarga `compute-Cobb-angle.py` del commit `72c712f`, comprueba su SHA-256, fija la dependencia Tiger en el commit `4c63f6d` y verifica que cada máscara usada sea idéntica a la de `masks.zip`. Con eso, las 447 máscaras devolvieron un ángulo (mediana por secuencia entre 6,6° y 6,7°). Para que el script funcione en NumPy 2 (la versión actual de Colab) hizo falta una adaptación de una línea, tomar la parte real de `np.linalg.eig`; antes de adoptarla se comprobó que da los mismos ángulos que el script sin modificar en NumPy 1.26. El procesamiento guarda cada resultado al terminarlo, de modo que se puede retomar si Colab se desconecta.

### 3. Herramientas para ver qué hace el algoritmo

El script original solo devuelve un número por serie. Para poder revisarlo caso por caso, el cuaderno 02 agrega celdas visuales que usan los mismos planos que calcula el script, sin cambiar su método:

- **Vista previa** de las máscaras de un estudio en sus tres secuencias, sobre la RM cuando la imagen está disponible, con su proyección coronal.
- **Panel del algoritmo**, con los platillos que estima en cada disco y el par que elige para el ángulo, junto con la inclinación sagital y coronal de esas caras.
- **Celda interactiva** para elegir a mano el par de discos y comparar el ángulo resultante con el del script.
- **Nomenclatura de etiquetas** de SPIDER explicada en el propio cuaderno: la numeración va de abajo hacia arriba y no equivale a niveles anatómicos (L1–L5) sin más información.

## Trabajo realizado en la segunda semana
### 4. El disco más caudal en las 447 series (cuaderno 03)

El caso del estudio 162 planteó una pregunta: ¿se trata de un caso aislado o la cara inferior del disco más caudal también influye en el ángulo calculado en otras series? Para investigarlo, el cuaderno 03 vuelve a ejecutar el script sobre las 447 máscaras y verifica que reproduce exactamente los resultados de la primera semana. Además, guarda los planos estimados para las 6294 caras de disco en `planos_por_disco.csv`, lo que permite explorar variantes del cálculo sin tener que volver a ejecutar el algoritmo original.

A partir de estos planos se evalúan tres variantes exploratorias:

- **A. Exclusión de la cara inferior del disco 201:** se repite el cálculo original, pero se excluye esta cara de la selección del par que define el ángulo.
- **B. Ángulo alternativo de cada cara:** se utiliza arcsen(n<sub>x</sub>) en lugar de la fórmula original del script, arctan(n<sub>x</sub>/n<sub>z</sub>).
- **AB. Combinación de ambas variantes:** se excluye la cara inferior del disco 201 y se utiliza la fórmula alternativa para calcular la inclinación de las caras restantes.

Estas variantes se plantean para estudiar la sensibilidad del resultado a la selección de las caras y a la fórmula utilizada. No forman parte del método publicado ni se proponen como correcciones validadas del algoritmo.

Para evitar duplicar observaciones, el análisis se realiza sobre las 340 máscaras únicas: 107 parejas T1/T2 comparten exactamente el mismo archivo de máscara.

### 5. Robustez frente al grosor de corte (cuaderno 04)

El cuaderno 04 estudia cómo influye el grosor de corte en el ángulo calculado mediante tres enfoques complementarios, ordenados desde el análisis descriptivo hasta un experimento controlado.

Primero, describe la distribución de los ángulos según el grosor de corte y el grupo de adquisición, teniendo en cuenta que ambos factores pueden estar relacionados. Después, compara las series T2 SPACE con las series estándar del mismo estudio para caracterizar las diferencias entre adquisiciones. Por último, realiza un experimento de remuestreo en el que cada una de las 41 máscaras T2 SPACE se transforma para simular cortes de 3,3 y 4,4 mm, utilizando dos métodos de remuestreo y tres posiciones iniciales del corte. En total, se obtienen 533 ejecuciones del script para este experimento.

El cuaderno también evalúa el acuerdo entre series mediante el método de Bland–Altman, cuantifica cuánto de la diferencia observada puede asociarse al efecto del grosor en el experimento controlado y calcula intervalos de confianza mediante bootstrap. La combinación de estos enfoques permite distinguir el efecto que se observa en los datos de aquel que puede atribuirse más directamente al grosor de corte bajo las condiciones del experimento.

## Trabajo realizado en la tercera semana
 
### 6. Segmentación automática frente a manual (cuaderno 05)
 
Hasta este punto, el cálculo del ángulo se había realizado sobre las máscaras manuales de SPIDER, revisadas y corregidas a mano por los anotadores del dataset. Sin embargo, en una aplicación automatizada no se dispondría de estas máscaras de antemano: sería necesario generarlas mediante un segmentador automático. Por eso, en el cuaderno 05 se evaluó cuánto cambia el ángulo de Cobb al utilizar máscaras generadas por dos herramientas públicas en lugar de las máscaras manuales.
 
Se compararon **SPIDER-Baseline-IIS**, el modelo de referencia del reto SPIDER, y **TotalSpineSeg**, de NeuroPoly, utilizando ambos modelos tal como fueron publicados, sin entrenarlos ni modificarlos. Cada uno se fijó a una versión concreta y sus pesos se verificaron por su huella antes de usarlos. Como los dos numeran los discos en sentido contrario a SPIDER, sus máscaras se renumeraron por la altura de cada estructura y después se procesaron con el mismo script fijado. El ángulo de cada máscara automática se comparó con el de la máscara manual de la misma serie, con las dos reglas de selección de caras de disco y emparejando los discos por posición, porque un segmentador puede omitir alguno. El cuaderno marca automáticamente las segmentaciones sospechosas (posible disco omitido, discos sin pareja o muy pequeños) y compara también la T1 y la T2 de un mismo estudio.
 
No entrené ningún modelo, los dos segmentadores se usaron tal como los publicaron sus autores. Por límites de cómputo, SPIDER-Baseline-IIS corrió en Kaggle y TotalSpineSeg en Colab, salvo 23 series que también corrieron en Kaggle, con el mismo código, los mismos pesos y la misma configuración. Los registros de la corrida de SPIDER-Baseline-IIS quedaron como hojas de cálculo en Drive y no se publican, y los de las 23 series de TotalSpineSeg en Kaggle no se conservaron; los detalles están en `docs/fuentes_externas.md`.
 
### 7. Ángulo medido en los platillos vertebrales (cuaderno 06)
 
El script mide el ángulo en las caras de los discos, mientras que el método de Cobb se traza sobre los platillos vertebrales. Por eso, el cuaderno 06 aísla el cuerpo de cada vértebra en las 340 máscaras manuales únicas, ajusta un plano a cada platillo y compara el ángulo resultante con las dos reglas de caras de disco, reutilizando los planos guardados en el cuaderno 03.

Esta medición es una propuesta exploratoria del proyecto, no parte del método publicado. En su versión final exige que cada punto del platillo esté a menos de 3 mm del disco que toca; esa condición se agregó después de una primera corrida en la que el ajuste falló en algunas máscaras (hallazgo 10), como 53_t1; la primera corrida se conserva en `salidas/resultados_semana3/06_cobb_por_platillos/version_sin_contacto/` y el cuaderno mide cuánto cambió el resultado con la corrección.

## Hallazgos preliminares

Los resultados de esta etapa son descriptivos y exploratorios. SPIDER no proporciona mediciones de referencia del ángulo de Cobb realizadas por observadores humanos, por lo que no es posible estimar la exactitud del algoritmo frente a una referencia clínica. Tampoco se aplica un umbral para clasificar las series como escolióticas o no escolióticas. El objetivo es caracterizar el comportamiento del algoritmo y explorar qué factores pueden influir en sus resultados.

### 1. La cara inferior del disco más caudal influye en muchas series, aunque el caso extremo sigue siendo excepcional
La cara inferior del disco 201 el disco más caudal de la máscara, probablemente correspondiente a L5–S1, aunque la etiqueta no permite establecer esa equivalencia anatómica por sí sola forma parte del par seleccionado por el script en 141 de las 340 máscaras únicas (41,5 %). La proporción es similar en las secuencias T1, T2 y T2 SPACE.

Al excluir esta cara mediante la variante A, el ángulo máximo disminuye una mediana de 1,44° en esas 141 máscaras (rango intercuartílico: 0,65°–2,64°). La reducción supera los 2° en 55 máscaras y los 5° en solo 5. El estudio 162 constituye el caso más extremo: el ángulo pasa de 36,87° a 11,59° en T2 SPACE y de 34,57° a 10,76° en T1.

En la primera semana se reportó que el ángulo bajaba hasta 1,8°–2,4° al elegir a mano otro par de discos (202–209). Ese resultado corresponde a una intervención distinta: al excluir únicamente la cara inferior del disco 201, el algoritmo selecciona el par 204–209. Por tanto, las dos cifras no deben compararse como si evaluaran la misma modificación.

### 2. La fórmula original amplifica la inclinación de la cara inferior del disco 201, pero no explica por sí sola su selección
La cara inferior del disco 201 presenta una inclinación sagital considerablemente mayor que las caras inferiores de los demás discos: la mediana de la inclinación absoluta es de aproximadamente 33°–34°, frente a 7,8° en las otras caras.

Las dos fórmulas evaluadas se relacionan mediante la identidad

<p align="center">tan θ<sub>script</sub> = tan θ<sub>B</sub> / cos φ</p>

donde θ<sub>B</sub> = arcsen(n<sub>x</sub>) y φ representa la inclinación sagital. En consecuencia, la fórmula original amplifica la tangente del ángulo coronal en las caras con una inclinación sagital pronunciada. Para la cara inferior del disco 201, el factor de amplificación 1/cos φ tiene una mediana de 1,197, frente a 1,011 para las demás caras.

Sin embargo, este efecto no basta para explicar por qué el algoritmo selecciona unas caras del disco 201 y no otras. Las caras seleccionadas y no seleccionadas presentan inclinaciones sagitales similares (medianas de 33,9° y 33,2°, respectivamente), pero las seleccionadas muestran una mayor inclinación lateral incluso al utilizar la fórmula alternativa basada en arcsen(n<sub>x</sub>): las medianas son de 2,7° y 1,3°.

Además, la reducción del ángulo asociada a la variante A presenta una correlación de Spearman mayor con la inclinación coronal de la cara (0,51) que con su inclinación sagital (0,20). Tampoco se observa evidencia de que las caras seleccionadas hayan sido ajustadas utilizando menos vértices que las demás.

Por su parte, la variante B modifica el ángulo una mediana de solo 0,20°. En conjunto, estos resultados sugieren que la selección de la cara y su inclinación coronal tienen mayor relevancia para el cambio observado que la sustitución aislada de la fórmula angular.

### 3. El grosor de corte modifica el ángulo, pero el efecto es pequeño y aproximadamente proporcional
En el experimento de remuestreo, aumentar el grosor de corte de las mismas máscaras T2 SPACE reduce el ángulo calculado una mediana de 0,22° para cortes de 3,3 mm (IC del 95 %: 0,16°–0,34°) y de 0,40° para cortes de 4,4 mm (IC del 95 %: 0,29°–0,48°). La reducción máxima observada es de 2,94°.

En términos relativos, las reducciones medianas son del 3,3 % y del 4,8 %, respectivamente. El ángulo coronal de cada cara se multiplica por un factor aproximadamente constante 0,967 para 3,3 mm y 0,95 para 4,4 mm, y el ángulo calculado por el algoritmo refleja ese comportamiento.

La posición inicial de los cortes también modifica el resultado en una magnitud comparable a la del grosor, mientras que las diferencias entre los dos métodos de remuestreo son pequeñas. Los cambios en el par seleccionado se concentran en casos con ángulos de 9,22° o menos, en los que dos pares presentan valores muy próximos.

Estos resultados indican que el grosor influye en la medición, pero su efecto aislado es relativamente pequeño en este experimento. No obstante, el resultado depende también de cómo se sitúan los cortes y de la geometría de las caras reconstruidas.

### 4. Entre series del mismo estudio, el grosor explica poco de la variabilidad observada
Al comparar las series estándar con las T2 SPACE del mismo estudio, se obtiene un sesgo de −0,32° y unos límites de acuerdo del 95 % de −3,09° a 2,44°. Al restringir el análisis a las comparaciones en las que ambas máscaras contienen el mismo número de discos, el sesgo es de −0,51° y los límites de acuerdo van de −2,59° a 1,58°.

El efecto del grosor observado en el experimento controlado predice casi exactamente la diferencia mediana entre las series: −0,28° frente a −0,29° observados en esa comparación. Sin embargo, la varianza de las diferencias predichas por el grosor es de 0,14, frente a 1,99 para las diferencias observadas.

Por tanto, aunque el grosor explica casi todo el desplazamiento sistemático entre las series, explica poco de la dispersión total. Entre los factores que podrían contribuir a esa variabilidad están las diferencias de segmentación entre adquisiciones, la secuencia utilizada, los cambios de posición del paciente y las diferencias en la cobertura de la máscara. Con estos datos no es posible determinar cuánto aporta cada factor por separado.

### 5. Una parte importante de las parejas T1/T2 comparte exactamente la misma máscara
En 107 de las 190 parejas T1/T2 correspondientes a un mismo estudio, las máscaras son idénticas byte a byte. En esas parejas, el ángulo calculado es necesariamente idéntico cuando se aplica el mismo algoritmo, por lo que no constituyen observaciones independientes de la variabilidad entre segmentaciones.

En las 83 parejas restantes, cuyas máscaras sí son distintas, la mediana de la diferencia absoluta entre los ángulos T1 y T2 es de 0,48°, y la diferencia máxima alcanza los 7,43°.

Esta distinción es importante al interpretar la concordancia entre secuencias ya que una parte de la igualdad observada se debe a que se utiliza exactamente la misma máscara, no necesariamente a que el algoritmo produzca resultados equivalentes a partir de segmentaciones independientes.

**Corrección tras la respuesta de los autores.** En los cuadernos 02 y 03 se dijo que el artículo de SPIDER no explica por qué hay máscaras idénticas. Jasper van der Graaf aclaró en el issue que, en cada estudio, se elegía la mejor segmentación entre la T1 y la T2, se corregía a mano y se reutilizaba para la otra secuencia cuando coincidía con ella. Por lo tanto, las parejas idénticas son una decisión de la anotación y no un error de los archivos.

### 6. La cobertura de la máscara también condiciona el ángulo calculado
La diferencia máxima de 7,43° entre las parejas T1/T2 corresponde al estudio 35. La máscara T2 cubre únicamente los discos 201–203 y produce un ángulo de 15,41°, mientras que la máscara T1 incluye nueve discos y produce un ángulo de 7,97°.

Cuando cambia el número de discos disponibles, también cambia el conjunto de pares que el algoritmo puede evaluar. Por ello, el máximo seleccionado puede corresponder a pares diferentes en cada secuencia, lo que limita la interpretación directa de la diferencia como un efecto exclusivo de la secuencia o de la segmentación.

Este caso ilustra que la cobertura anatómica representada en la máscara es otro factor que debe considerarse al comparar los resultados entre adquisiciones.

**Actualización de la tercera semana.** El cuaderno 05 confirmó que la máscara parcial de 35_t2 se debe al campo de visión de la serie y no a una segmentación incompleta, en los resultados obtenido se observó que la T1 y la T2 cubren casi la misma longitud (unos 299 mm), pero el campo de la T2 está desplazado unos 158 mm hacia caudal, y los dos segmentadores automáticos también encuentran solo tres discos en ella.

### 7. La segmentación automática suele cambiar poco el ángulo, pero puede presentar errores importantes

En comparación con las máscaras manuales, ambos segmentadores produjeron diferencias pequeñas en la mayoría de los casos. Con la regla del artículo, la mitad de las diferencias no superó 0,44° con SPIDER-Baseline-IIS ni 0,61° con TotalSpineSeg, y nueve de cada diez quedaron por debajo de 1,55° y 1,68°, respectivamente; con la regla del script, las cifras son parecidas. La principal diferencia entre las herramientas no está tanto en el comportamiento habitual como en los errores que pueden producir.

TotalSpineSeg no omitió discos según los criterios de evaluación del cuaderno, y su ángulo prácticamente no tuvo sesgo respecto al de la máscara manual, siguiendo la regla del artículo, la diferencia media fue de 0,03°, con límites de acuerdo de aproximadamente ±2,2°. Las mayores discrepancias aparecieron en series que no recibieron ninguna marca de calidad, es decir, que los controles automáticos no habrían detectado. El caso más claro fue el estudio 65, en el que las tres series presentaron ángulos entre 4,0° y 6,6° superiores a los calculados con la máscara manual. Al revisar las segmentaciones, se observó que el modelo representaba con mayor inclinación la cara superior del disco más caudal.

SPIDER-Baseline-IIS mostró un acuerdo incluso más estrecho cuando la segmentación era adecuada, al excluir su peor caso, las diferencias se situaron entre −2,0° y 1,6°. Sin embargo, presentó fallos que afectaron directamente al cálculo. Se detectaron posibles discos omitidos en 21 series; en 29_t2 y 74_t2 solo se segmentó un disco, y en 64_t1 se identificaron únicamente dos de los siete esperados. El caso más llamativo fue 167_t1, donde el ángulo calculado alcanzó 73,2°, frente a 7,1° con la máscara manual. La causa fue la presencia de un plano casi vertical junto a un disco omitido.

Estos resultados muestran que una diferencia angular pequeña en la mayoría de las imágenes no garantiza un funcionamiento fiable en todos los casos. Por ello, una herramienta que calcule el ángulo a partir de segmentaciones automáticas debería incorporar controles de calidad capaces de detectar discos ausentes, planos anómalos y resultados potencialmente incorrectos antes de entregar una medición.

Las cifras deben interpretarse como estimaciones optimistas del rendimiento, ambos segmentadores fueron entrenados con datos de SPIDER y no se dispone de un ángulo de referencia medido independientemente por especialistas para esta evaluación.

### 8. Los discos que definen el ángulo son menos estables que el valor angular

Aunque el ángulo calculado suele cambiar poco, los discos que determinan su valor máximo no siempre son los mismos. Con los dos segmentadores automáticos, el par de discos seleccionado coincidió con el de la máscara manual en solo el 64 % de las series con SPIDER-Baseline-IIS y el 57 % con TotalSpineSeg, con la regla del artículo. Al cambiar de regla o contar solo los discos presentes en las dos máscaras, la coincidencia nunca superó el 68 %, de modo que en al menos un tercio de las series el par cambia.

El cuaderno 06 permite entender esta diferencia. En aproximadamente tres de cada cuatro máscaras existen varios pares de discos cuyo ángulo queda a menos de 1° del máximo. Además, la diferencia mediana entre el mayor ángulo y el segundo mayor es de apenas 0,46°. En estas condiciones, una pequeña variación en la segmentación o en el ajuste de los planos puede cambiar cuál de los pares resulta seleccionado, sin modificar sustancialmente el ángulo final.

También se evaluó la reproducibilidad entre las secuencias T1 y T2 de un mismo estudio. Al segmentarlas y procesarlas por separado, las diferencias angulares fueron del orden de ±1,5° a 2°, una variabilidad comparable a la observada al utilizar distintas máscaras manuales.

En conjunto, estos resultados indican que el valor del ángulo puede ser relativamente estable incluso cuando cambia el par de discos que lo determina. Por tanto, conviene evaluar por separado la reproducibilidad de la medición angular y la estabilidad de los niveles anatómicos seleccionados.

### 9. La medición basada en platillos vertebrales concuerda con la regla del artículo

Se exploró una alternativa para calcular el ángulo a partir de los platillos vertebrales, en lugar de utilizar directamente las caras de los discos. Con la versión final del método, la inclinación de cada platillo quedó próxima a la de la cara del disco correspondiente, con límites de acuerdo de aproximadamente ±1,4°.

El ángulo calculado mediante los platillos fue, en promedio, 0,26° mayor que el obtenido con la regla del artículo (IC del 95 %: 0,13°–0,40°). Los límites de acuerdo se situaron entre −1,7° y 2,2°. Además, la reproducibilidad entre las secuencias T1 y T2 de un mismo estudio fue similar a la de la regla del artículo: aproximadamente ±1,6° frente a ±1,45°.

La comparación con la regla implementada en el script original mostró un acuerdo menor, con límites de −3,5° a 3,3°. Esta diferencia se explica, al menos en parte, porque la regla del script usa la otra cara de cada disco, la que no está en contacto con los platillos que se comparan.

Aunque los resultados respaldan la coherencia geométrica del método alternativo, el acuerdo entre ambos no constituye una validación independiente. El platillo vertebral y la cara del disco son superficies enfrentadas de una misma interfaz anatómica, por lo que es esperable que sus inclinaciones estén relacionadas.

Revisando el estudio 162 se observa un resultado diferente, el ángulo elevado se mantuvo al medir sobre los platillos, con valores de 23,7° y 25,9°. Esto indica que la curvatura observada no se explica únicamente por el ajuste de las caras de los discos. En cambio, los grados adicionales que aparecen con la regla del script proceden de la cara inferior del disco 201, en contacto con el sacro que es una superficie que no cuenta con un platillo vertebral correspondiente en las máscaras de SPIDER, porque el sacro no forma parte de la segmentación utilizada.

### 10. Se corrigió el método de medición por platillos y se documentó el cambio

La primera versión del método basado en platillos aceptaba cualquier superficie del cuerpo vertebral cuya orientación se pareciera a la de un platillo. Esto podía fallar cuando la etiqueta de una vértebra se extendía más allá de su platillo.

Un ejemplo fue el estudio 53_t1, donde la etiqueta de la vértebra 1 rodeaba al disco 201. Como consecuencia, el plano ajustado combinaba dos superficies distintas y producía un ángulo de 18,1°, frente a los 1,8° obtenidos con la regla del artículo.

Para corregirlo, se incorporó una condición adicional la cual consistia que el platillo seleccionado debía estar en contacto con el disco correspondiente. Con este cambio, el ángulo disminuyó en promedio 1,25° por máscara (IC del 95 %: 0,98°–1,54°).

La simulación incluida en el cuaderno 06 ayuda a explicar este comportamiento. Cuando aumenta el ruido en los planos, también aumenta la posibilidad de que el mayor ángulo observado sea artificialmente elevado, incluso si los planos individuales no presentan un sesgo sistemático. Con un ruido de 1,5° en cada cara, el máximo aumenta en promedio 1,42°, muy cerca del sesgo de 1,5° que tenía la primera versión frente a la regla del artículo. Por tanto, seleccionar el máximo entre varios pares puede amplificar pequeñas imprecisiones geométricas.

Se conservaron los resultados de ambas versiones para dejar constancia del problema identificado, la corrección aplicada y su efecto sobre las mediciones. La primera corrida está en `salidas/resultados_semana3/06_cobb_por_platillos/version_sin_contacto/`.

### Respuesta de los autores del algoritmo original

Esta semana también llegó la respuesta a las dudas sobre la implementación publicada que se plantearon en el issue DIAGNijmegen/cobb-angle-algorithm#1. Las respondió Jasper van der Graaf el autor del articulo de referencia.

Según su respuesta, el código publicado corresponde al utilizado en el artículo. La opción largest_angle=False estaba destinada a un análisis de consenso cuyos datos no llegaron a publicarse. Tampoco fue posible confirmar qué versión de Tiger se utilizó originalmente, dado que el código data de 2022.

El autor señaló, además, que la inclinación en el plano sagital es una limitación general de la medición de Cobb proyectada y explicó que las máscaras idénticas entre T1 y T2 se relacionan con el procedimiento de anotación descrito en el hallazgo 5.

Aunque el repositorio ya no cuenta con mantenimiento activo, quedó abierta la posibilidad de proponer cambios en dos puntos del script. Esta respuesta permitió aclarar varias decisiones de implementación y distinguir las limitaciones del método de los problemas propios de su reproducción.

### Pregunta abierta: la cara del extremo craneal de la máscara

En 115 de las 340 máscaras únicas, la cara superior del par seleccionado pertenece al disco más craneal de la máscara. En estos casos, la cara puede encontrarse cerca del límite del campo de visión y estar segmentada de forma incompleta.

Este aspecto queda fuera del análisis de la segunda semana, cuyo objetivo es estudiar la influencia de la cara inferior del disco más caudal y la robustez frente al grosor de corte. No obstante, constituye una línea de investigación pendiente: sería útil determinar en qué medida la cobertura parcial de los discos situados en los extremos de la máscara influye en la selección del par y en el ángulo final.

Los resultados y archivos necesarios para explorar esta cuestión están disponibles en `salidas/resultados_semana2/03_disco_caudal_y_variantes/`. Cualquier comentario, sugerencia o contribución para continuar este análisis es bienvenido en los issues del repositorio.

Los detalles metodológicos, las figuras y la interpretación de cada experimento se encuentran en los cuadernos de `notebooks/`; las tablas de resultados están disponibles en `salidas/`.

## Revisión de alcance (línea paralela de la etapa 1)

Protocolo registrado en OSF el 12-oct-2026: *Automated and semi-automated measurement of coronal spinal curvature and detection of scoliosis on MRI and CT in adults: a scoping review protocol*. doi:[10.17605/OSF.IO/WXQ5G](https://doi.org/10.17605/OSF.IO/WXQ5G) · proyecto [osf.io/5pm9q](https://osf.io/5pm9q). Pregunta, criterios PCC y búsqueda de registros existentes en [`docs/revision_alcance/`](docs/revision_alcance/).

## Cómo ejecutar

Los datos de SPIDER **no** no están incluidos en este repositorio ni se descargan automáticamente desde los cuadernos. Antes de empezar, es necesario descargar el conjunto de datos desde Zenodo (DOI: 10.5281/zenodo.10159290, versión v4) y guardarlo en Google Drive, respetando la estructura de carpetas indicada en la primera celda de cada cuaderno.

Una vez configurado el acceso a los archivos, se puede abrir cada cuaderno en Google Colab y ejecutar Entorno de ejecución → Reiniciar y ejecutar todo. Los cuadernos verifican las sumas MD5 de los datos y la huella SHA-256 del script antes de utilizarlos, lo que permite comprobar que los archivos corresponden a las versiones previstas.

Los cuadernos deben ejecutarse en orden, ya que los posteriores utilizan resultados generados por los anteriores. En particular, el cuaderno 04 necesita el inventario del 01 y la tabla de variantes del 03. Los cuadernos 05 y 06 también requieren el inventario del 01, los planos y la tabla de variantes del 03.

En las pruebas realizadas con Colab gratuito, los tiempos aproximados de ejecución fueron los siguientes:

- Cuaderno 02: una hora y media.
- Cuaderno 03: dos horas.
- Cuaderno 04: tres horas.
- Cuaderno 06: 40 minutos.

Los cuadernos guardan los resultados a medida que completan cada etapa y permiten continuar a partir de los resultados existentes si la sesión de Colab se interrumpe. Los tiempos indicados son orientativos y pueden variar según los recursos disponibles y las condiciones de ejecución.

El cuaderno 05 requiere consideraciones adicionales. Además de las máscaras manuales, necesita las 447 imágenes de SPIDER para generar las segmentaciones automáticas. Esta etapa requiere GPU y puede distribuirse en varias sesiones. En las pruebas, el procesamiento tomó entre 2 y 13 minutos por serie con SPIDER-Baseline-IIS y entre 1 y 2 minutos con TotalSpineSeg.

Para evitar ejecutar este proceso por accidente, las celdas de segmentación solo se activan al establecer CORRER_SEGMENTACION = True. Una vez generadas y guardadas las máscaras automáticas en Google Drive, el resto del cuaderno puede ejecutarse sin GPU.

Las máscaras automáticas no se incluyen en el repositorio porque pueden generarse nuevamente a partir de los datos originales y del cuaderno correspondiente.

## Datos, código y trabajos de referencia

- SPIDER: van der Graaf JW *et al.* *Sci Data* 2024;11:264. doi:[10.1038/s41597-024-03090-w](https://doi.org/10.1038/s41597-024-03090-w). Datos: doi:[10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290) (CC-BY 4.0).
- Método original: van der Graaf JW *et al.* *Eur Radiol* 2024;34(9):5748-5757. doi:[10.1007/s00330-024-10616-8](https://doi.org/10.1007/s00330-024-10616-8). Código: [DIAGNijmegen/cobb-angle-algorithm](https://github.com/DIAGNijmegen/cobb-angle-algorithm) (Apache-2.0), commit `72c712f`.
- Aplicación poblacional: Niglas M et al. Eur Spine J 2026. doi:10.1007/s00586-026-10239-1.
- Segmentador SPIDER-Baseline-IIS: DIAGNijmegen/SPIDER-Baseline-IIS (Apache-2.0), commit `438049a`. Método: Lessmann N et al. Med Image Anal 2019;53:142-155. doi:10.1016/j.media.2019.02.005.
- Segmentador TotalSpineSeg: neuropoly/totalspineseg (LGPL-3.0), versión `20260807` con los pesos `r20260730`; basado en nnU-Net (Isensee F et al. Nat Methods 2021;18:203-211).
- Método de Cobb: Cobb JR. Outline for the study of scoliosis. Instr Course Lect 1948;5:261-275.
- Versiones exactas de todo el código y los datos usados: [`docs/fuentes_externas.md`](docs/fuentes_externas.md).

## Cómo citar

Nossa Díaz, E. F. (2026). *Cobb coronal en RM lumbar sagital: reproducción abierta y prueba de robustez* (versión v0.0.1) [Software]. Zenodo. https://doi.org/10.5281/zenodo.23410109

Para citar el proyecto en general (todas las versiones), usa el concept DOI [10.5281/zenodo.23410108](https://doi.org/10.5281/zenodo.23410108). También puedes usar `CITATION.cff` o el botón *Cite this repository* de GitHub. Cada versión publicada recibe su propio DOI en Zenodo.

## Licencia

Código bajo [Apache-2.0](LICENSE). Los datos de SPIDER conservan su licencia CC-BY 4.0 y deben citarse según lo indican sus autores.

---

## English summary

Research-only, open and independent reproduction of automated coronal Cobb angle measurement on routine sagittal lumbar MRI (van der Graaf et al., Eur Radiol 2024), using the public SPIDER dataset, plus a robustness analysis across slice thickness, sequence (T1/T2) and acquisition site. **Not a medical device; not for diagnosis.**

Week 1: a verified inventory of SPIDER (counts match the Sci Data paper; age is available for only 41 of 218 patients; no hospital column, so site is approximated by scanner), and a pinned, checksum-verified run of the published script (commit `72c712f`) on all 447 masks, plus visual and interactive notebook cells to inspect which disc planes drive each angle. Preliminary, descriptive findings: (1) in some cases the maximum angle is driven by the lower face of the most caudal disc when it is strongly tilted in the sagittal plane (study 162: 34.6°–36.9° vs. 1.8°–2.4° with another disc pair); (2) 107 of 190 T1/T2 pairs share byte-identical masks; (3) mask coverage changes the result (study 35). Questions were sent to the authors in [DIAGNijmegen/cobb-angle-algorithm#1](https://github.com/DIAGNijmegen/cobb-angle-algorithm/issues/1). A parallel scoping review is registered on OSF (doi:[10.17605/OSF.IO/WXQ5G](https://doi.org/10.17605/OSF.IO/WXQ5G)).

Week 2, all descriptive (SPIDER has no reference Cobb angle): (1) the lower face of the most caudal disc (label 201) is part of the selected pair in 141 of 340 unique masks (41.5%); removing it lowers the angle by a median of 1.44°, with study 162 as the extreme case (36.87° to 11.59°). (2) The script's formula, arctan(n<sub>x</sub>/n<sub>z</sub>), relates exactly to arcsin(n<sub>x</sub>) through the face's sagittal tilt and inflates that face's tangent by about 20%, but the selected faces also carry more true lateral tilt. (3) Simulating 3.3 and 4.4 mm slices on the 41 high-resolution masks lowers the angle by a median of 0.22° and 0.40° (about 3–5%, proportional to the angle, maximum 2.94°). (4) Between the T2 SPACE and the standard series of the same patient, limits of agreement are about ±3°; slice thickness explains the median bias but little of the spread. Questions and results were shared with the authors in DIAGNijmegen/cobb-angle-algorithm#1. A parallel scoping review is registered on OSF (doi:10.17605/OSF.IO/WXQ5G).

Week 3, also descriptive: (1) Automatic masks from two public segmenters (SPIDER-Baseline-IIS and TotalSpineSeg, both used as published; no model was trained here) usually change the angle little compared with the manual masks (half of the differences under 0.44° with SPIDER-Baseline-IIS and 0.61° with TotalSpineSeg; limits of agreement about ±2.2° for TotalSpineSeg), but failures can be severe: SPIDER-Baseline-IIS skipped discs in some series and in one case gave 73.2° instead of 7.1°. Both segmenters were trained on SPIDER, so these are optimistic bounds. (2) The disc pair that defines the angle is much less stable than the angle itself: in three out of four masks several pairs lie within 1° of the maximum. (3) An exploratory endplate-based Cobb angle, requiring each endplate to touch its disc, stays within −1.7° to 2.2° of the article's disc-face rule and is as reproducible between T1 and T2; since endplate and disc face are two sides of the same interface, this agreement is partly expected. The large angle of study 162 persists on the endplates; the extra degrees of the script's rule come from the disc face that touches the sacrum. A first version of the endplate method failed on some masks and was corrected; the correction lowered the endplate angle by 1.25° on average, and both runs are kept. The authors answered the questions in DIAGNijmegen/cobb-angle-algorithm#1: among other points, identical T1/T2 masks come from reusing the best corrected segmentation for both sequences.
