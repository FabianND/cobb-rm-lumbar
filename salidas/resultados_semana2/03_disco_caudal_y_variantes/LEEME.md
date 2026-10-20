# 03 · El disco más caudal (201) y tres variantes del ángulo

Resultados de `notebooks/03_disco_caudal_y_variantes.ipynb`. Solo investigación; no es para diagnóstico.
Los ángulos salen de las máscaras manuales de SPIDER v4 con `compute-Cobb-angle.py` (commit `72c712f`);
no hay Cobb de referencia, así que ninguna variante se presenta como la correcta.

| Archivo | Qué contiene |
|-|-|
| `planos_por_disco.csv` | Una fila por cara de disco y serie: normal y punto del plano del script, ángulo coronal del script, arcsen(nx), inclinación sagital y si la cara forma parte del par elegido |
| `registro_corrida.csv` | Una fila por serie: ángulo del script, número de discos, estado y tiempo |
| `angulos_variantes.csv` | Una fila por serie: ángulo y par de discos del original y de las variantes A (sin 201), B (arcsen) y AB, diferencias y huella de la máscara |
| `resumen_disco_201.csv` | Series en que el par original incluye el disco 201 y series que cambian de par, con y sin máscaras duplicadas |
| `resumen_inclinacion_sagital.csv`, `figura_inclinacion_sagital.png` | Inclinación sagital de la cara inferior del 201 frente a las demás caras inferiores |
| `resumen_variantes.csv`, `figura_original_vs_variantes.png` | Cuánto cambia el ángulo con cada variante |
| `resumen_inclinacion_lateral.csv`, `figura_inclinacion_lateral.png` | Inclinación lateral de la cara inferior del 201 frente a las demás, con las dos fórmulas |
| `figura_relacion_formulas.png` | Comprobación de la relación exacta entre la fórmula del script y arcsen(nx) en cada cara |
| `efecto_A_vs_cara_201.csv`, `figura_efecto_A_vs_cara_201.png` | Reducción del ángulo al retirar el 201 frente a la inclinación de su cara inferior |
| `resumen_vertices_por_cara.csv`, `figura_vertices_por_cara.png` | Número de vértices usados en el ajuste de cada cara, absoluto y relativo a su serie |
| `figuras_variantes/` | Una figura por serie con el par que elige cada variante |
| `casos_extremos/` | Panel y tabla de los casos con mayor diferencia |
| `entorno.json` | Versiones, commits y huellas de la corrida |

Las figuras originales del script (sin variantes) son idénticas a las de la semana 1 y están en
[`resultados_semana1/02_compute-Cobb-angle/figuras/`](../../resultados_semana1/02_compute-Cobb-angle/figuras/).
