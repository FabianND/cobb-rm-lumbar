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
| 1 | Preguntas a los autores del script y del dataset ([DIAGNijmegen/cobb-angle-algorithm#1](https://github.com/DIAGNijmegen/cobb-angle-algorithm/issues/1); seguimiento en [#1](https://github.com/FabianND/cobb-rm-lumbar/issues/1)) | Abierto, esperando de respuesta |

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

Esta distinción es importante al interpretar la concordancia entre secuencias: una parte de la igualdad observada se debe a que se utiliza exactamente la misma máscara, no necesariamente a que el algoritmo produzca resultados equivalentes a partir de segmentaciones independientes.

### 6. La cobertura de la máscara también condiciona el ángulo calculado
La diferencia máxima de 7,43° entre las parejas T1/T2 corresponde al estudio 35. La máscara T2 cubre únicamente los discos 201–203 y produce un ángulo de 15,41°, mientras que la máscara T1 incluye nueve discos y produce un ángulo de 7,97°.

Cuando cambia el número de discos disponibles, también cambia el conjunto de pares que el algoritmo puede evaluar. Por ello, el máximo seleccionado puede corresponder a pares diferentes en cada secuencia, lo que limita la interpretación directa de la diferencia como un efecto exclusivo de la secuencia o de la segmentación.

Este caso ilustra que la cobertura anatómica representada en la máscara es otro factor que debe considerarse al comparar los resultados entre adquisiciones.

### Pregunta abierta: la cara del extremo craneal de la máscara

En 115 de las 340 máscaras únicas, la cara superior del par seleccionado pertenece al disco más craneal de la máscara. En estos casos, la cara puede encontrarse cerca del límite del campo de visión y estar segmentada de forma incompleta.

Este aspecto queda fuera del análisis de la segunda semana, cuyo objetivo es estudiar la influencia de la cara inferior del disco más caudal y la robustez frente al grosor de corte. No obstante, constituye una línea de investigación pendiente: sería útil determinar en qué medida la cobertura parcial de los discos situados en los extremos de la máscara influye en la selección del par y en el ángulo final.

Los resultados y archivos necesarios para explorar esta cuestión están disponibles en `salidas/resultados_semana2/03_disco_caudal_y_variantes/`. Cualquier comentario, sugerencia o contribución para continuar este análisis es bienvenido en los issues del repositorio.

Los detalles metodológicos, las figuras y la interpretación de cada experimento se encuentran en los cuadernos de `notebooks/`; las tablas de resultados están disponibles en `salidas/`.

## Revisión de alcance (línea paralela de la etapa 1)

Protocolo registrado en OSF el 12-oct-2026: *Automated and semi-automated measurement of coronal spinal curvature and detection of scoliosis on MRI and CT in adults: a scoping review protocol*. doi:[10.17605/OSF.IO/WXQ5G](https://doi.org/10.17605/OSF.IO/WXQ5G) · proyecto [osf.io/5pm9q](https://osf.io/5pm9q). Pregunta, criterios PCC y búsqueda de registros existentes en [`docs/revision_alcance/`](docs/revision_alcance/).

## Cómo ejecutar

Los datos **no** están en este repositorio y los cuadernos no los descargan por ti. Antes de ejecutar, descarga SPIDER desde Zenodo (doi:[10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290), versión v4) y guárdalo en Google Drive con la estructura que indica la primera celda de cada cuaderno. Luego abre el cuaderno en Google Colab y usa *Entorno de ejecución → Reiniciar y ejecutar todo*. Los cuadernos verifican las sumas MD5 de los datos y la huella SHA-256 del script antes de usarlos.

Los cuadernos se corren en orden, porque cada uno usa salidas de los anteriores: el 04 necesita el inventario del 01 y la tabla de variantes del 03. En Colab gratuito, el 02 tarda cerca de hora y media, el 03 cerca de dos horas y el 04 unas tres horas; los tres guardan cada resultado al terminarlo y retoman donde iban si Colab se desconecta.

## Datos, código y trabajos de referencia

- SPIDER: van der Graaf JW *et al.* *Sci Data* 2024;11:264. doi:[10.1038/s41597-024-03090-w](https://doi.org/10.1038/s41597-024-03090-w). Datos: doi:[10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290) (CC-BY 4.0).
- Método original: van der Graaf JW *et al.* *Eur Radiol* 2024;34(9):5748-5757. doi:[10.1007/s00330-024-10616-8](https://doi.org/10.1007/s00330-024-10616-8). Código: [DIAGNijmegen/cobb-angle-algorithm](https://github.com/DIAGNijmegen/cobb-angle-algorithm) (Apache-2.0), commit `72c712f`.
- Aplicación poblacional: Niglas M *et al.* *Eur Spine J* 2026. doi:[10.1007/s00586-026-10239-1](https://doi.org/10.1007/s00586-026-10239-1).
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
