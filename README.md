# Cobb coronal en RM lumbar sagital: reproducción abierta y prueba de robustez

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
| 1 | Preguntas a los autores del script y del dataset ([DIAGNijmegen/cobb-angle-algorithm#1](https://github.com/DIAGNijmegen/cobb-angle-algorithm/issues/1); seguimiento en [#1](https://github.com/FabianND/cobb-rm-lumbar/issues/1)) | Abierto - esperando de respuesta |

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

## Hallazgos preliminares

Son resultados **descriptivos**. SPIDER no incluye un ángulo de Cobb medido por personas, así que aquí no se calcula exactitud ni se usa ningún umbral para llamar "escoliosis" a una serie.

1. **El disco más caudal puede inflar el ángulo.** En el estudio 162 el script devuelve 34,6° (T1/T2) y 36,9° (T2 SPACE), definidos por la cara inferior del disco más caudal (etiqueta 201, probablemente L5–S1), muy inclinada en el plano sagital (≈ −59°), mientras la columna se ve recta en la proyección coronal; con los mismos planos y el par de discos 202–209 el ángulo es 1,8°–2,4°. La explicación propuesta (una inclinación sagital fuerte combinada con una leve rotación axial infla el ángulo coronal calculado como arctan(n<sub>x</sub>/n<sub>z</sub>)) es una inferencia geométrica que falta confirmar.
2. **Muchas parejas T1/T2 comparten máscara.** En 107 de 190 parejas T1/T2 de un mismo estudio las dos máscaras son idénticas byte a byte, así que su ángulo es igual por construcción. En las 83 parejas con máscaras distintas, la diferencia T1 − T2 tuvo mediana absoluta de 0,48° y máximo de 7,43°.
3. **La cobertura de la máscara cambia el resultado.** Ese máximo corresponde al estudio 35: la máscara de T2 solo cubre los discos 201–203 y da 15,41°, frente a 7,97° en T1 con nueve discos. Con menos niveles segmentados, el script elige el máximo entre otros pares.

Los detalles y las figuras están en `notebooks/02_compute_cobb_angle.ipynb`; las tablas, en `salidas/resultados_semana1/`.

## Revisión de alcance (línea paralela de la etapa 1)

Protocolo registrado en OSF el 12-oct-2026: *Automated and semi-automated measurement of coronal spinal curvature and detection of scoliosis on MRI and CT in adults: a scoping review protocol*. doi:[10.17605/OSF.IO/WXQ5G](https://doi.org/10.17605/OSF.IO/WXQ5G) · proyecto [osf.io/5pm9q](https://osf.io/5pm9q). Pregunta, criterios PCC y búsqueda de registros existentes en [`docs/revision_alcance/`](docs/revision_alcance/).

## Cómo ejecutar

Los datos **no** están en este repositorio y los cuadernos no los descargan por ti. Antes de ejecutar, descarga SPIDER desde Zenodo (doi:[10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290), versión v4) y guárdalo en Google Drive con la estructura que indica la primera celda de cada cuaderno. Luego abre el cuaderno en Google Colab y usa *Entorno de ejecución → Reiniciar y ejecutar todo*. Los cuadernos verifican las sumas MD5 de los datos y la huella SHA-256 del script antes de usarlos. El cuaderno 02 procesa las 447 máscaras en cerca de hora y media en Colab gratuito.

## Datos, código y trabajos de referencia

- SPIDER: van der Graaf JW *et al.* *Sci Data* 2024;11:264. doi:[10.1038/s41597-024-03090-w](https://doi.org/10.1038/s41597-024-03090-w). Datos: doi:[10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290) (CC-BY 4.0).
- Método original: van der Graaf JW *et al.* *Eur Radiol* 2024;34(9):5748-5757. doi:[10.1007/s00330-024-10616-8](https://doi.org/10.1007/s00330-024-10616-8). Código: [DIAGNijmegen/cobb-angle-algorithm](https://github.com/DIAGNijmegen/cobb-angle-algorithm) (Apache-2.0), commit `72c712f`.
- Aplicación poblacional: Niglas M *et al.* *Eur Spine J* 2026. doi:[10.1007/s00586-026-10239-1](https://doi.org/10.1007/s00586-026-10239-1).
- Versiones exactas de todo el código y los datos usados: [`docs/fuentes_externas.md`](docs/fuentes_externas.md).

## Cómo citar

Ver `CITATION.cff` o el botón *Cite this repository* de GitHub. Cada versión publicada recibe un DOI en Zenodo.

## Licencia

Código bajo [Apache-2.0](LICENSE). Los datos de SPIDER conservan su licencia CC-BY 4.0 y deben citarse según lo indican sus autores.

---

## English summary

Research-only, open and independent reproduction of automated coronal Cobb angle measurement on routine sagittal lumbar MRI (van der Graaf et al., Eur Radiol 2024), using the public SPIDER dataset, plus a robustness analysis across slice thickness, sequence (T1/T2) and acquisition site. **Not a medical device; not for diagnosis.**

Week 1: a verified inventory of SPIDER (counts match the Sci Data paper; age is available for only 41 of 218 patients; no hospital column, so site is approximated by scanner), and a pinned, checksum-verified run of the published script (commit `72c712f`) on all 447 masks, plus visual and interactive notebook cells to inspect which disc planes drive each angle. Preliminary, descriptive findings: (1) in some cases the maximum angle is driven by the lower face of the most caudal disc when it is strongly tilted in the sagittal plane (study 162: 34.6°–36.9° vs. 1.8°–2.4° with another disc pair); (2) 107 of 190 T1/T2 pairs share byte-identical masks; (3) mask coverage changes the result (study 35). Questions were sent to the authors in [DIAGNijmegen/cobb-angle-algorithm#1](https://github.com/DIAGNijmegen/cobb-angle-algorithm/issues/1). A parallel scoping review is registered on OSF (doi:[10.17605/OSF.IO/WXQ5G](https://doi.org/10.17605/OSF.IO/WXQ5G)).
