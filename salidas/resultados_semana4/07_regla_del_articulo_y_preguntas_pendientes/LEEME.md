# 07 · La regla correcta y las preguntas pendientes

Resultados de `notebooks/07_regla_del_articulo_y_preguntas_pendientes.ipynb`. Solo investigación; no es para diagnóstico.
Cierra las preguntas abiertas de los cuadernos 01 a 06 con sus resultados y con las 340 máscaras manuales únicas de SPIDER v4; no se vuelve a correr el script.

| Archivo | Qué contiene |
|-|-|
| `centros_frente_a_tabla1.csv`, `hospital_inferido_por_serie.csv` | Grupos de escáner frente a la Tabla 1 del artículo de SPIDER y hospital inferido para cada serie |
| `recorte_de_niveles.csv`, `resumen_recorte_de_niveles.csv`, `parejas_por_cobertura.csv`, `figura_recorte_de_niveles.png` | El ángulo según cuántos discos entran en la máscara |
| `reglas_por_mascara.csv` | Ángulo y par de discos con la regla del script, la del artículo, la del script recorriendo los discos de arriba hacia abajo y la del artículo con arcsen(nx) |
| `script_frente_a_articulo.csv`, `figura_script_frente_a_articulo.png` | Cuánto cambia el ángulo al pasar de la regla del script a la del artículo |
| `variantes_frente_a_articulo.csv`, `resumen_variantes_frente_a_articulo.csv`, `figura_variantes_frente_a_articulo.png` | Variantes A, B y AB del cuaderno 03, regla del artículo y platillos del cuaderno 06 |
| `banco_formula_desarrollo.csv`, `banco_formula_prueba.csv`, `resumen_banco_formula.csv`, `figura_banco_formula.png` | Banco de pruebas de la fórmula: cinco candidatas frente al borde proyectado, en discos sintéticos y en discos reales rotados |
| `proyeccion_por_disco_manual.csv`, `proyeccion_por_disco_tss.csv`, `proyeccion_por_disco_iis.csv` | Ángulo del borde superior e inferior de cada disco en la proyección coronal, en las máscaras manuales y automáticas |
| `cobb_por_candidata_manual.csv`, `cobb_por_candidata_tss.csv`, `cobb_por_candidata_iis.csv`, `reproducibilidad_por_candidata.csv`, `figura_reproducibilidad_por_candidata.png` | Ángulo de Cobb (regla del artículo) con cada candidata y su reproducibilidad entre segmentaciones |
| `cobertura_por_disco.csv` | Para cada disco, si toca el borde craneal, caudal o lateral de la imagen |
| `extremo_craneal_por_mascara.csv`, `resumen_extremo_craneal.csv`, `panel_extremo_craneal.png` | Uso del disco más craneal por cada regla, si está cortado y cuánto cambia el ángulo sin él |
| `grosor_con_regla_del_articulo.csv`, `resumen_grosor_con_regla_del_articulo.csv`, `space_frente_a_estandar_con_regla_del_articulo.csv`, `resumen_space_frente_a_estandar.csv` | Las cifras del cuaderno 04 con la regla del artículo |
| `entrenamiento_frente_a_validacion.csv`, `figura_entrenamiento_frente_a_validacion.png` | Acuerdo de cada segmentador con la máscara manual en las particiones de SPIDER |
| `direccion_manual_frente_a_automatica.csv`, `resumen_direccion_por_inclinacion.csv`, `direccion_platillo_frente_a_cara.csv`, `estudio_65_por_superficie.csv`, `figura_direccion_extremo_caudal.png` | Inclinación total y dirección de cada cara: máscaras automáticas, platillos y el estudio 65 |
| `platillos_por_distancia.csv`, `registro_platillos_por_distancia.csv`, `cobb_platillos_por_distancia.csv`, `resumen_distancia_de_contacto.csv`, `figura_distancia_de_contacto.png` | Platillos y ángulo por platillos con 2, 3 y 4 mm de distancia de contacto |
| `entorno.json` | Versiones, commits, huellas y parámetros |

Regla del script: max |cara inferior del disco de abajo − cara superior del de arriba|; regla del artículo: max |cara superior del disco de abajo − cara inferior del de arriba|; discos numerados de caudal a craneal.
Disco cortado: toca el borde craneal o el primer o último corte sagital de la imagen reorientada. Inclinación total y dirección: tan(arctan(nx/nz)) = tan(i) · sen(a).
Bootstrap de 2000 repeticiones por estudio, semilla 2026.
