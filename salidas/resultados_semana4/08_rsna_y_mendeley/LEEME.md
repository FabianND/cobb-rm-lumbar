# 08 · RSNA y Mendeley: inventario y preparación de la segmentación

Resultados de `notebooks/08_rsna_y_mendeley.ipynb`. Solo investigación; no es para diagnóstico.

Los términos de uso de RSNA prohíben compartir o redistribuir cualquier parte de sus datos. Por eso aquí solo hay
resúmenes agregados de RSNA; las tablas por estudio, serie e imagen se quedan en una carpeta privada que no se publica.
Mendeley tiene licencia CC BY 4.0 (Sudirman et al., doi:10.17632/k57fr854j2.2 y doi:10.17632/s6bgczr8s2.2).

| Archivo | Qué contiene |
|-|-|
| `estructura_de_los_zip.csv` | Archivos y bytes por carpeta de primer nivel y extensión en cada zip |
| `rsna_resumen_series_sagitales.csv` | Series sagitales de entrenamiento de RSNA por tipo de secuencia: cortes, grosor, espaciado, cobertura lateral, píxel |
| `rsna_escaneres.csv`, `rsna_grosores.csv` | Series sagitales de RSNA por fabricante y campo (vacío: RSNA no conserva esos campos), y por grosor de corte |
| `rsna_niveles_marcados.csv` | Estudios de RSNA con la posición de cada nivel marcada, por tipo de serie |
| `mendeley_inventario/` | Cabeceras de Mendeley: tandas por imagen, cabecera completa de la primera imagen de cada serie y resumen por serie |
| `mendeley_resumen_series_sagitales.csv` | Series sagitales de Mendeley, con las mismas columnas que RSNA |
| `mendeley_notas_*.csv` | Las notas de los radiólogos, una tabla por hoja del Excel original |
| `mendeley_menciones_escoliosis.csv` | Cada mención de escoliosis en las notas, con su contexto y una marca de posible negación |
| `comparacion_con_spider.csv`, `comparacion_con_spider.png` | Grosor, espaciado, cortes y cobertura lateral de las series sagitales de SPIDER, RSNA y Mendeley |
| `conversion_mendeley.csv` | Conversión a NIfTI de cada serie sagital de Mendeley, con sus comprobaciones y la huella del volumen |
| `conversion_resumen.csv` | Series convertidas y avisos de la conversión, por conjunto |
| `seleccion_mendeley.csv` | Series T1 y T2 sagitales candidatas de Mendeley y la elegida en cada paciente |
| `seleccion_resumen.csv` | Series candidatas, elegidas y estudios con T1 y T2, por conjunto |
| `listas_resumen.csv` | Estudios, series y horas de GPU estimadas en cada lista de trabajo |
| `entorno.json` | Versiones, tamaños y huellas de los archivos de entrada, semillas y versión de TotalSpineSeg |

La prueba de TotalSpineSeg en CPU (celda 17) no terminó en Colab, así que no hay tabla ni figuras de esa prueba.
Los NIfTI de Mendeley están en `MyDrive/PRL/content/datos/mendeley/nifti_sagital/`. Las listas, los NIfTI, el
inventario detallado de RSNA y las máscaras que produce Kaggle están en carpetas privadas de `MyDrive/PRL/content/datos/`.
