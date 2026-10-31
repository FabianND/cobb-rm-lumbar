# 09 · Segmentación externa: revisión técnica y plan de análisis

Resultados de `notebooks/09_segmentacion_externa.ipynb`. Solo investigación; no es para diagnóstico.

Los términos de uso de RSNA prohíben compartir o redistribuir cualquier parte de sus datos: aquí solo hay resúmenes
agregados de RSNA. Las tablas por estudio, serie o punto, las máscaras y su traducción están en carpetas privadas.
Mendeley (doi:10.17632/k57fr854j2.2) y SPIDER tienen licencia CC BY 4.0.

| Archivo | Qué contiene |
|-|-|
| `kaggle_resumen.csv` | Series por lista y conjunto: en la lista, correctas, con error, huellas y geometría distintas, tiempo |
| `kaggle_errores_por_tipo.csv` | Errores de la segmentación por tipo, sin identificadores |
| `geometria_rsna_resumen.csv` | Geometría de RSNA: lo que daba la lectura con GDCM y lo que se tomó de las cabeceras |
| `marcas_resumen.csv` | Porcentaje de series con cada marca de calidad, por conjunto y secuencia |
| `marcas_mendeley.csv` | Marcas de calidad de cada serie de Mendeley |
| `mendeley_series_cervicales.csv` | Series de Mendeley cuya máscara es cervical y la serie lumbar del mismo estudio que se usa |
| `mendeley_sin_discos_lumbares.csv` | Máscaras de Mendeley sin ningún disco lumbar, con su espaciado y los discos que traen |
| `niveles_rsna_resumen.csv`, `niveles_rsna_por_nivel.csv`, `niveles_rsna_corrimientos.csv` | Numeración de TotalSpineSeg frente a las coordenadas de RSNA |
| `spider_error_caras_por_serie.csv` | Error de orientación de las caras de disco y Dice frente a la máscara manual de SPIDER |
| `comparacion_t1_t2.csv`, `comparacion_t1_t2.png`, `decision_secuencia.json` | Comparación pareada T1 frente a T2 y secuencia principal |
| `numeracion_t1_t2_resumen.csv`, `numeracion_t1_t2_corrimientos.csv`, `numeracion_t1_t2_mendeley.csv` | Numeración de los discos en la T1 frente a la T2 del mismo estudio |
| `sexta_lumbar_resumen.csv`, `sexta_lumbar_t1_t2.csv`, `niveles_rsna_segun_sexta_lumbar.csv` | Sexta vértebra lumbar y disco L5-L6 |
| `fallos_rsna_medianas.csv`, `fallos_rsna_por_cuartil.csv` | Adquisición de las series de RSNA y series sin máscara |
| `rsna_huellas_protocolo_resumen.csv` | Huellas de protocolo de RSNA (combinaciones de parámetros de adquisición) |
| `cobertura_lateral_resumen.csv` | Cobertura lateral de las series frente a los discos que tocan el borde lateral |
| `muestra_cuaderno_10.csv`, `mendeley_sexo_edad_muestra.csv` | Estudios que llegan al cuaderno 10 y precisión esperada de los límites de acuerdo |
| `plan_analisis_cuaderno_10.md`, `plan_analisis_cuaderno_10.sha256` | Plan de análisis del cuaderno 10 para registrar en OSF, y su huella |
| `entorno.json` | Versiones, parámetros y huellas de las entradas |

Secuencia principal decidida por la regla: T1. Huella del plan: 14548723494df98ce3fa0e78135a7c7dbe1317e985dadbdee97943f3e35f970b.
Plan registrado en OSF el 31-oct-2026: doi:10.17605/OSF.IO/KP5DU (https://doi.org/10.17605/OSF.IO/KP5DU).
