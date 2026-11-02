# 10 · Ángulo coronal lumbar en RSNA y Mendeley: propiedades de medición

Resultados de `notebooks/10_angulo_coronal_externo.ipynb`. Solo investigación; no es para diagnóstico. El ángulo es un
"ángulo coronal lumbar en decúbito estimado en RM sagital", no el ángulo de Cobb clínico, y ningún conjunto trae ángulo de referencia.

Plan registrado en OSF antes de calcular ningún ángulo: doi:10.17605/OSF.IO/KP5DU (https://doi.org/10.17605/OSF.IO/KP5DU),
archivo `plan_analisis_cuaderno_10.md` del cuaderno 09, SHA-256 14548723494df98ce3fa0e78135a7c7dbe1317e985dadbdee97943f3e35f970b.

Los términos de uso de RSNA prohíben compartir o redistribuir cualquier parte de sus datos: aquí solo hay resúmenes
agregados de RSNA (las figuras de RSNA son densidades, sin puntos por estudio). Las tablas por estudio o serie de RSNA
están en una carpeta privada. Mendeley (doi:10.17632/k57fr854j2.2) y SPIDER tienen licencia CC BY 4.0.

| Archivo | Qué contiene |
|-|-|
| `control_positivo_resumen.csv`, `control_positivo_spider_por_cara.csv`, `control_positivo_spider_por_serie.csv`, `control_positivo_decision.json` | Control positivo de la versión del script con la caja de cada disco, en las 447 series de SPIDER (manuales y TotalSpineSeg) |
| `panel_control_*.png` | Serie de prueba de Mendeley con las caras elegidas, los centroides y las etiquetas |
| `planos_resumen.csv`, `angulos_disponibles.csv` | Máscaras con planos y centroides, y series con ángulo, por conjunto y secuencia |
| `angulos_por_serie_mendeley.csv` | Ángulo de cada serie de Mendeley con las tres fórmulas, par elegido, signo, centroides y piso de ruido |
| `comprobacion_signo.csv` | Comprobación del signo con columnas sintéticas de lado conocido |
| `marcas_resumen.csv`, `marcas_por_estudio_mendeley.csv` | Marcas de calidad del plan |
| `analisis1_acuerdo_t1_t2.csv`, `analisis1_hipotesis_H1.csv`, `analisis1_bland_altman.png` | Análisis 1: acuerdo T1–T2 e hipótesis H1 |
| `analisis2_error_por_cara.csv`, `analisis2_piso_de_ruido_por_discos.csv`, `caras_pareadas_t1_t2_mendeley.csv` | Análisis 2: error por cara σ y piso de ruido |
| `analisis3_zona_de_indecision.csv`, `analisis3_zona_de_indecision.png` | Análisis 3: discrepancia en la clasificación ≥10° |
| `analisis4_inclinacion_sagital.csv` | Análisis 4: desacuerdo según la inclinación sagital |
| `analisis5_distribucion.csv`, `analisis5_mendeley_sexo_edad.csv`, `analisis5_distribucion.png` | Análisis 5: distribución y proporciones ≥10° |
| `analisis6_comprobaciones_informes.json`, `analisis6_pacientes_con_escoliosis_en_el_informe.csv`, `analisis6_auc_descriptiva.csv`, `analisis6_panel_pacientes_con_escoliosis.png` | Análisis 6: notas de radiólogos de Mendeley |
| `analisis7_factores_por_cuartil.csv`, `analisis7_factores_spearman.csv`, `analisis7_rsna_huellas_con_20_o_mas_estudios.csv` | Análisis 7: factores de adquisición |
| `analisis8_caras_frente_a_centroides.csv`, `analisis8_caras_frente_a_centroides.png` | Análisis 8: caras de disco frente a centroides |
| `exploratorio_tipo_de_punto_rsna.csv`, `exploratorio_acuerdo_t1_t2_centroides.csv` | Exploratorios (fuera del plan registrado) |
| `exploratorio_precision_sin_escala.csv`, `exploratorio_precision_sin_escala_diferencias.csv`, `exploratorio_analisis6_sin_0196_0197.csv` | Exploratorios agregados después de ver los resultados: precisión sin el efecto de la escala y análisis 6 sin los estudios 0196 y 0197 |
| `entorno.json` | Versiones, parámetros, decisión del control positivo y huellas de las entradas |

Versión del script usada: caja. Hipótesis H1: completo: se cumple; sin_marcas: se cumple.
