# 04 · Robustez del ángulo de Cobb frente al grosor de corte

Resultados de `notebooks/04_robustez_grosor_de_corte.ipynb`. Solo investigación; no es para diagnóstico.
Los ángulos salen de las máscaras manuales de SPIDER v4 con `compute-Cobb-angle.py` (commit `72c712f`).
Los cortes gruesos se simulan sobre las 41 máscaras T2 SPACE; no hay Cobb de referencia.

| Archivo | Qué contiene |
|-|-|
| `angulo_por_grosor.csv`, `angulo_por_grupo_adquisicion.csv`, `angulo_avanto_fit_por_grosor.csv`, `figura_angulo_por_grosor_y_grupo.png` | Ángulo original de las máscaras únicas por grosor de corte y por grupo de adquisición (cuaderno 03) |
| `space_frente_a_estandar.csv`, `figura_space_frente_a_estandar.png` | Ángulo de cada T2 SPACE frente al de las series estándar del mismo estudio |
| `planos_engrosamiento.csv` | Una fila por cara de disco, serie y condición: normal y punto del plano, ángulos por cara y si la cara forma parte del par elegido |
| `registro_corrida.csv` | Una fila por serie y condición: ángulo del script, discos, cortes laterales, estado y tiempo |
| `angulos_engrosamiento.csv` | Una fila por serie y condición: ángulo y par de cada variante, base y diferencia respecto a la base |
| `resumen_por_grosor.csv`, `figura_base_frente_a_engrosada.png` | Cambio del ángulo original por grosor y método |
| `resumen_por_desfase.csv`, `figura_variacion_por_desfase.png` | Variación del ángulo según la posición del primer corte |
| `resumen_por_metodo.csv` | Diferencia entre vecino más cercano y etiqueta mayoritaria |
| `sensibilidad_por_variante.csv` | Cambio absoluto de cada variante del cuaderno 03 al engrosar |
| `casos_extremos/` | Panel y tabla de las máscaras con mayor cambio |
| `direccion_y_cambio_relativo.csv`, `cambio_por_tramo_de_angulo.csv` | Cuántas corridas bajan el ángulo, cambio relativo y cambio por tramo del ángulo base |
| `cambios_de_par_y_margen.csv`, `figura_proporcionalidad_y_pares.png` | Corridas con cambio de par por máscara y margen entre los dos mejores pares de la máscara fina |
| `ic_bootstrap.csv` | Intervalos de confianza del 95 % por bootstrap de máscaras o estudios para las medianas principales |
| `bland_altman_space_frente_a_estandar.csv`, `bland_altman_comparaciones.csv`, `figura_bland_altman.png` | Sesgo, límites de acuerdo y error absoluto medio entre la T2 SPACE y la serie estándar del mismo estudio |
| `grosor_frente_a_segmentacion.csv`, `resumen_grosor_frente_a_segmentacion.csv`, `figura_grosor_frente_a_segmentacion.png` | Diferencia observada entre series frente a la predicha solo por el grosor, y residuo |
| `mecanismo_por_cara.csv`, `figura_mecanismo_por_cara.png` | Cambio del ángulo coronal y sagital de cada cara de disco al engrosar |
| `entorno.json` | Versiones, commits, huellas y diseño del experimento |

Las máscaras engrosadas no se guardan: se regeneran con la función `engrosar` de la celda 8a.
