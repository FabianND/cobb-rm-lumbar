# 05 · Ángulo de Cobb con segmentación automática frente a manual

Resultados de `notebooks/05_segmentacion_automatica.ipynb`. Solo investigación; no es para diagnóstico.
Las máscaras automáticas no están aquí: se guardan en `MyDrive/PRL/content/datos/AutoSegments/` y pueden regenerarse con el cuaderno.

| Archivo | Qué contiene |
|-|-|
| `prueba_pocas_series/` | Prueba de los dos segmentadores en cuatro series: tiempos, discos, sentido de la numeración, panel y campo de visión del estudio 35 |
| `entorno_kaggle.json` | Entorno de la corrida de SPIDER-Baseline-IIS en Kaggle (los registros por serie quedaron como hojas de cálculo en Drive y no se publican) |
| `registro_segmentacion_tss.csv` | Corrida de TotalSpineSeg en Colab (424 series); las 23 series corridas en Kaggle no tienen registro |
| `traduccion_etiquetas_iis.csv`, `traduccion_etiquetas_tss.csv` | Equivalencia de cada etiqueta con la convención de SPIDER, altura, volumen y marca de disco pequeño |
| `registro_script_iis.csv`, `registro_script_tss.csv` | Estado y ángulo del script sobre cada máscara traducida |
| `planos_por_disco_iis.csv`, `planos_por_disco_tss.csv` | Plano de cada cara de disco, con las mismas columnas que el cuaderno 03 |
| `comparacion_por_serie.csv` | Una fila por serie y segmentador: discos, parejas, marcas de calidad y ángulos con cada regla y nivel |
| `acuerdo_manual_vs_auto.csv`, `bland_altman_completo.png`, `bland_altman_comunes.png` | Acuerdo con la máscara manual por segmentador, regla, nivel y subconjunto, con y sin series marcadas |
| `acuerdo_t1_t2.csv` | Acuerdo entre T1 y T2 del mismo estudio con cada tipo de máscara |
| `casos_167_t1_y_65_t1.png` | Panel de los dos casos comentados en la síntesis |
| `entorno.json` | Versiones, commits, huellas y parámetros de la comparación |

Umbrales de las marcas: pareja de discos a menos de 10 mm; posible disco omitido si un salto entre discos consecutivos supera 1.5 veces la mediana; disco pequeño si tiene menos de una cuarta parte del volumen mediano de los discos de su máscara.
