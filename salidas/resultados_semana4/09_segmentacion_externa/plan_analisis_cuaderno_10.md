# Plan de análisis del cuaderno 10: ángulo coronal lumbar en RSNA y Mendeley

Proyecto de investigación sobre la medición del ángulo coronal lumbar en RM sagital (repositorio FabianND/cobb-rm-lumbar). Este plan se generó en el cuaderno 09 el 2026-10-31, antes de calcular ningún ángulo coronal en RSNA o en Mendeley.

## 1. Pregunta y alcance
El objetivo es estudiar las propiedades de medición de un ángulo coronal lumbar calculado automáticamente a partir de
RM sagital de rutina en adultos, utilizando dos conjuntos externos, RSNA LumbarDISC y Lumbar Spine MRI Dataset de
Mendeley. La variable se denomina "ángulo coronal lumbar en decúbito estimado en RM sagital". No corresponde al
ángulo de Cobb clínico, que se mide en radiografías de pie. Ninguno de los dos conjuntos dispone de un ángulo de
referencia. Por tanto, este trabajo no evalúa exactitud diagnóstica, no estima una probabilidad de escoliosis y tampoco
entrena un modelo.

## 2. Datos
Se utilizarán las máscaras de TotalSpineSeg (paquete 20260807, pesos r20260730) correspondientes a una serie T1 y una
serie T2 sagitales por estudio, seleccionadas en el cuaderno 08. Las imágenes de RSNA se convirtieron utilizando la
geometría registrada en sus cabeceras DICOM. En 38 series de Mendeley (21 estudios) la serie elegida en el cuaderno 08 era cervical; 37 se cambiaron por la
serie lumbar de la misma secuencia del mismo estudio y la restante queda como no utilizable (cuaderno 09). Series con máscara utilizable (cuaderno 09): Mendeley T1 491 utilizables de 515, Mendeley T2
485 utilizables de 515, RSNA T1 1774 utilizables de 1973, RSNA T2/STIR 1780 utilizables de 1974. La unidad de análisis será el estudio, que corresponde a un paciente en ambos conjuntos. La T1 y la T2 del mismo estudio numeraron igual los discos lumbares en 99,2 % de los estudios de Mendeley y 98,7 % de los de RSNA. TotalSpineSeg marcó una sexta vértebra lumbar en 0,3 % de las máscaras de Mendeley y 0,4 % de las de RSNA. Estudios con las dos secuencias utilizables: 478 en Mendeley y 1.738 en RSNA (477 y 1.731 con la misma numeración en las dos máscaras), con los que la semiamplitud del IC 95 % de cada límite de acuerdo será de unas 0,15 y 0,08 desviaciones estándar de las diferencias. En RSNA, la huella de protocolo gruesa (matriz de la imagen y paso entre cortes redondeado a 0,5 mm) toma 90 valores en la T1 y 102 en la T2.

## 3. Secuencia principal
T1, decidida en el cuaderno 09 con una regla fijada el 30-oct-2026 (la T2 pasa a principal solo si es
mejor en al menos dos de tres medidas técnicas con IC 95 % que excluya la igualdad y no es peor en la tercera):
- Error de las caras en SPIDER (grados): diferencia T2 − T1 = -0,025 (IC 95 % -0,060 a 0,011), 190 estudios.
- Cinco niveles coinciden en RSNA (proporción): diferencia T2 − T1 = 0,077 (IC 95 % 0,063 a 0,092), 1895 estudios.
- Máscara utilizable en RSNA y Mendeley (proporción): diferencia T2 − T1 = 0,000 (IC 95 % -0,008 a 0,007), 2487 estudios.
La secuencia T2 también se analizará en su totalidad como corroboración. Los análisis por
paciente se presentarán para ambas secuencias.

## 4. Medición
Las máscaras se llevarán a la convención de numeración de SPIDER, de caudal a craneal. Los planos de las caras de
los discos se calcularán con el script
compute-Cobb-angle.py del repositorio DIAGNijmegen/cobb-angle-algorithm (commit
72c712f31e1f3069aef77b98b20af448bbc5615a, SHA-256 del archivo
4b6de7ca4f12b134dfb9fc6b373768a4a3b9a8763d66238b5798c7eaa7c89849) con la adaptación a NumPy 2 de los cuadernos 02 a 07
y una optimización de tiempo: la superficie de cada disco (marching cubes) se calcula sobre la caja que lo contiene, con
un vóxel de margen, y no sobre el volumen completo, y a sus vértices se les suma la posición de la caja; nada más del
script cambia. Antes de usarla en RSNA y Mendeley, esta versión se corre sobre todas las series de SPIDER y se compara
con los planos guardados en los cuadernos 03 (máscaras manuales) y 05 (TotalSpineSeg). Se considera equivalente si en
todas las caras la diferencia entre la normal guardada y la nueva es menor de 0,001° y en todas las series el ángulo del
script difiere menos de 0,001° del guardado. Si no se cumple, se usa el script sin la optimización. La comparación se
publica completa.
Las caras se emparejarán siguiendo la regla del artículo, que relaciona la cara superior del disco caudal con la cara
inferior del disco craneal. La fórmula principal utiliza el eje lateral proyectado, atan(nx·nz / (1 − nx²)). Como
referencia también se calcularán la fórmula del método publicado, arctan(nx/nz), y arcsen(nx). El ángulo de cada serie será el valor
máximo obtenido entre todos los pares. Como estimador independiente para estudiar la validez convergente, se calculará
el ángulo entre las tangentes de la curva de centroides de los cuerpos vertebrales en el plano coronal. El cuerpo
vertebral se aislará por delante del canal, siguiendo el procedimiento del cuaderno 06.

## 5. Criterios de calidad
Se identificarán las series con una máscara no utilizable según los criterios del cuaderno 09, menos de seis discos,
inclinación sagital superior a 30° en alguna de las caras del par seleccionado, disco cortado por el borde lateral o
craneal, numeración lumbar diferente entre T1 y T2 del mismo estudio, o presencia de una sexta vértebra lumbar en
alguna de las máscaras. Estas condiciones se registrarán como marcas de calidad, pero no serán motivos de exclusión
automática. Los resultados se presentarán tanto para el conjunto completo como para los estudios sin marcas.

## 6. Análisis previstos
1. Acuerdo T1–T2 del mismo estudio: sesgo, límites de acuerdo, coeficiente de repetibilidad e ICC(A,1), con IC 95 % por
   remuestreo de estudios (2.000 réplicas, semilla 2026); para la fórmula principal, para arctan(nx/nz) y para arcsen(nx).
   Hipótesis direccional (del cuaderno 07): el eje lateral tiene límites de acuerdo más estrechos que arctan. arcsen(nx)
   se reporta como referencia sin cambio de escala y no sustituye a la fórmula principal si la hipótesis no se cumple.
2. Error por cara: desviación estándar σ de la diferencia de inclinación coronal T1–T2 de caras emparejadas por nivel,
   dividida por √2. Piso de ruido: distribución simulada del ángulo máximo en una columna recta con el número de caras de
   cada serie y error σ.
3. Zona de indecisión: proporción de estudios en que T1 y T2 discrepan en la clasificación ≥10°, según el ángulo medio.
4. Desacuerdo T1–T2 según la inclinación sagital de las caras (por debajo y por encima de 30°).
5. Distribución del ángulo y proporción ≥10° por conjunto, observada y por encima del piso de ruido, con IC de
   Clopper-Pearson; en Mendeley, por sexo y por grupos de edad.
6. Notas de radiólogos de Mendeley: posición (rango) de los cinco pacientes con escoliosis informada, AUC exacta solo
   descriptiva y coincidencia del lado de la convexidad con el signo del ángulo; correspondencia informe–carpeta y posible
   duplicado de los informes 196 y 197 (comparando huellas de volumen).
7. Factores de adquisición (grosor, espaciado, tamaño del píxel, cobertura lateral) y huella de protocolo gruesa de RSNA
   (matriz de la imagen y paso entre cortes redondeado a 0,5 mm), que no equivale a una institución.
8. Acuerdo entre el ángulo por caras de disco y el estimador de centroides.

## 7. Desviaciones
Cualquier cambio respecto a este plan se reporta como desviación, con su motivo. Los análisis no previstos se presentan
como exploratorios.
