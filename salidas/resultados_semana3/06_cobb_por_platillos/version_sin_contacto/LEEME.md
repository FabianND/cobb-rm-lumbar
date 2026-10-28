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

Parámetros: platillo = puntos de la superficie del cuerpo con la normal a menos de 45° del eje de la vértebra;
mínimo de 50 puntos por plano; bootstrap de 2000 repeticiones por estudio, semilla 2026.
