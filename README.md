# Cobb coronal en RM lumbar sagital: reproducción abierta y prueba de robustez

> **Solo investigación. No es un dispositivo médico ni sirve para diagnóstico.** Nada en este repositorio debe usarse para tomar decisiones sobre pacientes.

*English summary below.*

## Pregunta

¿Se puede reproducir de forma independiente y abierta la medición automática del ángulo de Cobb coronal a partir de RM lumbar sagital de rutina en adultos, y qué tan estable es esa medición cuando cambian el grosor de corte, la secuencia (T1/T2) y el centro de adquisición?

## Alcance

Este proyecto está en su **etapa 1 (validación técnica con datos públicos)**. Trabaja sobre el dataset público SPIDER y no usa datos de pacientes de ninguna institución.

Lo que sí hace es reimplementar el método publicado por van der Graaf *et al.* (2024), documentar cada decisión y medir la variabilidad del resultado ante cambios técnicos de la imagen.

Lo que no hace es diagnosticar escoliosis, predecir su aparición o progresión, ni reemplazar la radiografía de pie. El valor medido es un **"Cobb coronal en decúbito en RM"**, que no equivale al Cobb radiográfico en bipedestación.

## Estado

| Semana | Entregable | Estado |
|---|---|---|
| 1 | Inventario descriptivo de SPIDER (`notebooks/01_inventario_spider.ipynb`) | en curso |

## Cómo ejecutar

Abrir `notebooks/01_inventario_spider.ipynb` en Google Colab y usar *Entorno de ejecución → Reiniciar y ejecutar todo*. El cuaderno descarga de Zenodo solo las máscaras y los archivos de resumen (unos 60 MB), verifica sus sumas MD5 y genera las tablas en `salidas/`. Los datos **no** se guardan en este repositorio.

## Datos y trabajos de referencia

- SPIDER: van der Graaf JW *et al.* *Sci Data* 2024;11:264. doi:[10.1038/s41597-024-03090-w](https://doi.org/10.1038/s41597-024-03090-w). Datos: doi:[10.5281/zenodo.10159290](https://doi.org/10.5281/zenodo.10159290) (CC-BY 4.0).
- Método original: van der Graaf JW *et al.* *Eur Radiol* 2024;34(9):5748-5757. doi:[10.1007/s00330-024-10616-8](https://doi.org/10.1007/s00330-024-10616-8). Código: [DIAGNijmegen/cobb-angle-algorithm](https://github.com/DIAGNijmegen/cobb-angle-algorithm) (Apache-2.0).
- Aplicación poblacional: Niglas M *et al.* *Eur Spine J* 2026. doi:[10.1007/s00586-026-10239-1](https://doi.org/10.1007/s00586-026-10239-1).

## Cómo citar

Ver `CITATION.cff` o el botón *Cite this repository* de GitHub. Cada versión publicada recibe un DOI en Zenodo.

## Licencia

Código bajo [Apache-2.0](LICENSE). Los datos de SPIDER conservan su licencia CC-BY 4.0 y deben citarse según lo indican sus autores.

---

## English summary

Research-only, open and independent reproduction of automated coronal Cobb angle measurement on routine sagittal lumbar MRI (van der Graaf et al., Eur Radiol 2024), using the public SPIDER dataset, plus a robustness analysis across slice thickness, sequence (T1/T2) and acquisition site. **Not a medical device; not for diagnosis.**
