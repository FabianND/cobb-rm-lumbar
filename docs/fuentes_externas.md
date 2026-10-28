# Fuentes externas usadas (registro de versiones)

|Fuente|Versión / commit|Licencia|Fecha de consulta|Huella|Notas|
|-|-|-|-|-|-|
|SPIDER (Zenodo 10.5281/zenodo.10159290)|v4|CC-BY 4.0|2-oct-2026|MD5 en `entorno.json`|Solo `overview.csv`, `radiological\_gradings.csv`, `masks.zip`|
|DIAGNijmegen/cobb-angle-algorithm · `compute-Cobb-angle.py`|commit: 72c712f31e1f3069aef77b98b20af448bbc5615a  (sin releases)|Apache-2.0 (`LICENSE.txt`)|2-oct-2026|SHA-256 del archivo: 4b6de7ca4f12b134dfb9fc6b373768a4a3b9a8763d66238b5798c7eaa7c89849 | mismo script sin modificar desde 2023|
|DIAGNijmegen/Tiger (dependencia del script)|rama/etiqueta `stable`, commit: 4c63f6d58ed3f8e7a0cec04b0352949f7b512919|Apache-2.0|2-oct-2026|||
|SimpleITK (cuaderno 04)|2.5.6|Apache-2.0|18-oct-2026||Se usa para leer, engrosar y escribir las máscaras en el experimento de grosor de corte|
|DIAGNijmegen/SPIDER-Baseline-IIS (cuaderno 05)|commit: 438049a8a679d04f5446c34676e8372fd7b86ead|Apache-2.0|24-oct-2026|SHA-256 de los pesos `experiments/SPIDER-Baseline/weights/999999.pkl`: 5925c72bde416f41ecbbd39b57d39fd174b973155a87baf4d89f2dd9a1a1e201 (coincide con el puntero de Git LFS del commit)|Segmentador de referencia del reto SPIDER; valores por defecto de `TestSpine.py` con `--export_original`|
|neuropoly/totalspineseg (cuaderno 05)|`totalspineseg==20260807` (PyPI); pesos de la release `r20260730`|LGPL-3.0|21-oct-2026|SHA-256 de `Dataset101_TotalSpineSeg_step1_r20260730.zip`: 781f81e8c94feccd3cef17d819ba5c293b506e9b1f2b106fc5e31b9dd85887b0 · `Dataset102_TotalSpineSeg_step2_r20260730.zip`: 494c640ab8cb25475bd0fc4338c0931d37079af9dd19403879335c3908c06b46|Instalado en un entorno virtual aparte dentro de Colab|
|nnunetv2 (dependencia de TotalSpineSeg)|2.6.2|Apache-2.0|24-oct-2026||Fijado en la instalación de TotalSpineSeg|
|kornia (dependencia de TotalSpineSeg)|0.8.2|Apache-2.0|24-oct-2026||Fijado porque las versiones posteriores quitaron un nombre que usa la herramienta|

## Entorno de ejecución
 
Los cuadernos corren en Google Colab y guardan en `entorno.json`, dentro de su carpeta de salidas, las versiones exactas de Python y de las librerías que usaron. Las corridas de los cuadernos 03 y 04 (18-oct-2026) usaron Python 3.13.16, NumPy 2.1.3, scikit-image 0.25.2, pandas 2.2.3 y matplotlib 3.10.0. Las de los cuadernos 05 (26-oct-2026) y 06 (27-oct-2026) usaron esas mismas versiones, más SciPy 1.16.3 y SimpleITK 2.5.6.
 
TotalSpineSeg corrió con el PyTorch de Colab (2.11.0, CUDA 13.0). Sus autores recomiendan PyTorch anterior a 2.6, así que esa combinación no es la que ellos probaron.
 
Por límites de cómputo, parte de la segmentación del cuaderno 05 corrió en Kaggle tanto series de SPIDER-Baselien-IIS como de TotalSpine, con el mismo codigo y misma configuración. 
