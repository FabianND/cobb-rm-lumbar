# Fuentes externas usadas (registro de versiones)

|Fuente|Versión / commit|Licencia|Fecha de consulta|Huella|Notas|
|-|-|-|-|-|-|
|SPIDER (Zenodo 10.5281/zenodo.10159290)|v4|CC-BY 4.0|2-oct-2026|MD5 en `entorno.json`|Solo `overview.csv`, `radiological\_gradings.csv`, `masks.zip`|
|DIAGNijmegen/cobb-angle-algorithm · `compute-Cobb-angle.py`|commit: 72c712f31e1f3069aef77b98b20af448bbc5615a  (sin releases)|Apache-2.0 (`LICENSE.txt`)|2-oct-2026|SHA-256 del archivo: 4b6de7ca4f12b134dfb9fc6b373768a4a3b9a8763d66238b5798c7eaa7c89849 | mismo script sin modificar desde 2023|
|DIAGNijmegen/Tiger (dependencia del script)|rama/etiqueta `stable`, commit: 4c63f6d58ed3f8e7a0cec04b0352949f7b512919|Apache-2.0|2-oct-2026|||
|SimpleITK (cuaderno 04)|2.5.6|Apache-2.0|18-oct-2026||Se usa para leer, engrosar y escribir las máscaras en el experimento de grosor de corte|

## Entorno de ejecución
 
Los cuadernos corren en Google Colab y guardan en `entorno.json`, dentro de su carpeta de salidas, las versiones exactas de Python y de las librerías que usaron. Las corridas de los cuadernos 03 y 04 (18-oct-2026) usaron Python 3.13.16, NumPy 2.1.3, scikit-image 0.25.2, pandas 2.2.3 y matplotlib 3.10.0.
