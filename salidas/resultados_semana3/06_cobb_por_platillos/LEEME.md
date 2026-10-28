# 06 · Ángulo de Cobb medido en los platillos vertebrales

Resultados de `notebooks/06_cobb_por_platillos.ipynb`. Solo investigación; no es para diagnóstico.
La medición por platillos es una propuesta exploratoria del proyecto, no el método publicado ni una medida validada.
Se usan las 340 máscaras manuales únicas de SPIDER v4; las caras de disco salen de `planos_por_disco.csv` del cuaderno 03.

| Archivo | Qué contiene |
|-|-|
| `panel_control_162_t1.png` | Cuerpo aislado y platillos de 162_t1, con las caras de disco del cuaderno 03 |
| `platillos_por_vertebra.csv` | Una fila por platillo: disco vecino, normal y punto del plano, puntos usados, inclinación lateral (fórmula del script) y sagital |
| `registro_platillos.csv` | Estado y tiempo de cada máscara |
| `platillo_vs_cara_de_disco.csv` | Cada platillo con la cara de disco que lo toca y la diferencia entre los dos |
| `acuerdo_platillo_vs_cara.csv`, `figura_platillo_vs_cara.png` | Acuerdo entre platillos y caras de disco por grupo y secuencia |
| `cobb_por_serie.csv` | Una fila por máscara: ángulo por platillos y su par, par de discos equivalente y ángulos y pares de las dos reglas de caras de disco |
| `acuerdo_cobb_platillos_vs_discos.csv`, `bland_altman_platillos_vs_discos.png` | Acuerdo del ángulo por platillos con cada regla de caras de disco |
| `panel_casos.png` | Estudio 162 y máscaras con mayor diferencia frente a la regla del artículo |
| `entorno.json` | Versiones, commits, huellas y parámetros |
| `acuerdo_t1_t2_por_medida.csv` | Acuerdo entre T1 y T2 del mismo estudio con platillos y con cada regla de caras de disco |
| `simulacion_ruido.csv` | Aumento del ángulo y cambio de par de la regla del artículo con ruido simulado en las caras de disco |
| `pares_candidatos.csv`, `figura_pares_candidatos.png` | Pares a menos de 1° del máximo en cada máscara, con las dos formas de medir |
| `panel_fallo_53_t1.png` | Puntos que toma el ajuste en el platillo que falla (53_t1) y en uno que funciona (162_t1) |
| `cambio_por_condicion_de_contacto.csv` | Ángulo por platillos de cada máscara con y sin la condición de contacto, y su diferencia |

Parámetros: platillo = puntos de la superficie del cuerpo con la normal a menos de 45° del eje de la vértebra y a menos de 3 mm de su disco vecino;
mínimo de 50 puntos por plano; bootstrap de 2000 repeticiones por estudio, semilla 2026.
