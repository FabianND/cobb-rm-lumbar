# Revisión de alcance, pregunta PCC y búsqueda de protocolos existentes

**Última actualización:** 3 de octubre de 2026

**Estado:** Registrado en OSF (12-oct-2026), doi:10.17605/OSF.IO/WXQ5G
**Etapa del proyecto:** etapa 1 (producto paralelo a la validación técnica con datos públicos). La revisión no depende de la etapa 2, pero sus resultados informarán el diseño de esa etapa, en particular la elección del estándar de referencia y de las condiciones técnicas que deben registrarse.



Guía metodológica: JBI Manual for Evidence Synthesis (capítulo de revisiones de alcance) y la lista de verificación PRISMA-ScR (Tricco *et al.*, *Ann Intern Med* 2018; doi:[10.7326/M18-0850](https://doi.org/10.7326/M18-0850)).

## 1\. Pregunta de investigación

> ¿Qué métodos automáticos o semiautomáticos se han publicado para medir la curvatura coronal de la columna (ángulo de Cobb u otra medida angular o geométrica explícita) o para detectar escoliosis en resonancia magnética o tomografía computarizada de adultos, frente a qué estándar de referencia se han validado (quién midió, sobre qué imagen y en qué posición del paciente) y qué características de las imágenes se han estudiado como fuente de variación?



La pregunta se ajustó el 3-oct-2026 después de revisar las revisiones y los protocolos existentes. El ajuste permitió definir con mayor precisión tres aspectos de interés para esta revisión: la detección además de la medición, las características del estándar de referencia y las condiciones técnicas de las imágenes.



## 2\. Elementos PCC y criterios de elegibilidad

|Elemento|Definición|Decisión|
|-|-|-|
|**P**oblación|Adultos (≥ 18 años), personas vivas|Los estudios con población mixta se incluyen solo si reportan los resultados de adultos por separado o permiten extraerlos. Los demás se registran como excluidos por población. Se excluyen estudios en cadáveres y fantomas.|
|**C**oncepto|Medición automática o semiautomática de la curvatura coronal (Cobb u otra medida angular o geométrica explícita) y detección de escoliosis|Se incluirán métodos que midan el ángulo de Cobb u otra medida explícita de la curvatura coronal. Los métodos que solo realicen segmentación o localización anatómica se incluirán cuando formen parte de un procedimiento destinado a detectar o medir la curvatura.|
|**C**ontexto|RM o TC, cualquier región de la columna, cualquier entorno clínico o de investigación|Se incluyen TC de baja dosis y TC de otros estudios (por ejemplo abdominales) por su interés para la detección oportunista.|
|Tipo de fuentes|Artículos científicos y artículos completos de congresos científicos.|Se incluirán artículos publicados en revistas revisadas por pares y artículos completos de congresos científicos. Las tesis y los preprints podrán consultarse como fuentes de apoyo, pero no se incluirán en la síntesis principal.|
|Periodo|Sin límite inicial de fecha|Desde el inicio de cada base hasta la fecha de la búsqueda definitiva, que se reportará. Si entre esa búsqueda y el envío del manuscrito pasan más de seis meses, la búsqueda se actualizará.|
|Idioma|Inglés y español|—|

### Variables de extracción

De cada estudio se extraerán la modalidad y la región de la columna; la secuencia o protocolo, la resolución en el plano y el grosor de corte; la población, el tamaño de muestra y el número de centros; el objetivo del método (detección de escoliosis, clasificación, medición del ángulo de Cobb, medición de otra curvatura geométrica, segmentación o localización anatómica); el método (segmentación, puntos de referencia o regresión directa) y si es automático o semiautomático; la definición del ángulo o de la medida geométrica; el estándar de referencia, especificando quién midió, sobre qué imagen y en qué posición del paciente (decúbito o bipedestación); las métricas (MAE, ICC de acuerdo absoluto, Bland-Altman y, para detección, sensibilidad y especificidad); las condiciones técnicas evaluadas como fuente de variación; la validación externa; y la disponibilidad de código y datos.



## 3\. Registro de la búsqueda de revisiones y protocolos existentes

|Fecha|Base|Términos exactos|Resultados|¿Protocolo o revisión igual o parecida?|Enlace|
|-|-|-|-|-|-|
|3-oct-2026|PubMed|`(Cobb OR scoliosis) AND (automated OR automatic OR "deep learning" OR "machine learning") AND (MRI OR "magnetic resonance" OR CT OR "computed tomography") AND (protocol\[ti] OR "scoping review"\[tiab] OR "systematic review"\[tiab])`|4|No se identificó un protocolo equivalente. La revisión más cercana es Zhu et al. (2024), que estudia la medición automatizada del ángulo de Cobb, pero se limita a radiografías.|[doi:10.1007/s43390-024-00954-4](https://doi.org/10.1007/s43390-024-00954-4)|
|3-oct-2026|PubMed (cribado)|`("Cobb angle" OR scoliosis OR "spinal curvature") AND (automated OR automatic OR "deep learning" OR "artificial intelligence") AND (MRI OR "magnetic resonance" OR "computed tomography" OR CT) AND (Review\[pt] OR "scoping review"\[tiab] OR "systematic review"\[tiab] OR "meta-analysis"\[tiab])`|12|No se identificó un protocolo equivalente. Los trabajos más cercanos son revisiones sobre medición del ángulo de Cobb, IA aplicada a la escoliosis e IA musculoesquelética. Ninguno se centra específicamente en métodos automatizados aplicados a RM y TC en adultos.|Jin: [doi:10.3390/s22093258](https://doi.org/10.3390/s22093258)<br>Zhang: [doi:10.3390/jcm12237382](https://doi.org/10.3390/jcm12237382)<br>Ruitenbeek: [doi:10.1007/s00256-024-04684-6](https://doi.org/10.1007/s00256-024-04684-6)|
|3-oct-2026|IEEE Xplore|`("All Metadata":"Cobb angle" OR "All Metadata":scoliosis OR "All Metadata":"spinal curvature") AND ("All Metadata":MRI OR "All Metadata":"magnetic resonance" OR "All Metadata":"computed tomography") AND ("All Metadata":review OR "All Metadata":survey)`|1|No se identificó un protocolo equivalente. Kumar et al. (2024) es una revisión sistemática relacionada con la identificación vertebral y la estimación del ángulo de Cobb, pero combina diferentes modalidades y grupos de edad y no presenta un protocolo registrado.|[doi:10.1109/ACCESS.2024.3353794](https://doi.org/10.1109/ACCESS.2024.3353794)|
|3-oct-2026|Scopus|`TITLE-ABS-KEY(("Cobb angle" OR scoliosis OR "spinal curvature" OR "coronal curvature") AND (automat\* OR "deep learning" OR "machine learning" OR "artificial intelligence") AND (mri OR "magnetic resonance" OR ct OR "computed tomography")) AND TITLE-ABS-KEY("scoping review" OR "systematic review" OR protocol)`|14|No se identificó un protocolo equivalente. Los resultados incluyen revisiones sobre IA y escoliosis, medición del ángulo de Cobb y progresión de la enfermedad. Ninguna se centra específicamente en la detección o medición automatizada en RM y TC de adultos.|—|
|3-oct-2026|PROSPERO|`("Cobb angle" OR scoliosis OR "spinal curvature" OR "coronal curvature") AND (automat\* OR "deep learning" OR "machine learning" OR "artificial intelligence") AND (mri OR "magnetic resonance" OR ct OR "computed tomography")`|89|No se identificó un protocolo equivalente. Se encontraron tres registros parcialmente relacionados, pero todos tienen un alcance más amplio. Ninguno se centra exclusivamente en RM y TC en adultos ni estudia las condiciones técnicas de las imágenes.|[CRD420251180554](https://www.crd.york.ac.uk/PROSPERO/view/CRD420251180554)<br>[CRD420251046877](https://www.crd.york.ac.uk/PROSPERO/view/CRD420251046877)<br>[CRD420261476402](https://www.crd.york.ac.uk/PROSPERO/view/CRD420261476402)|

Embase y Web of Science no se consultó por falta de acceso institucional; se declarará como limitación de la búsqueda de revisiones existentes.

## 4\. Revisiones registradas o publicadas relacionadas

### Registros en PROSPERO parcialmente superpuestos

|Registro|Autores|Alcance|Estado al 3-oct-2026|Diferencia con esta revisión|
|-|-|-|-|-|
|[CRD420251180554](https://www.crd.york.ac.uk/PROSPERO/view/CRD420251180554)|Qi, Yin, Li y Wang|Revisión sistemática y metaanálisis de la exactitud del Cobb automático con aprendizaje profundo en adolescentes y adultos; todas las modalidades agrupadas (radiografía, TC, RM, ecografía); solo en inglés. Desenlaces: R², MAE y sesgo.|En curso; fin previsto en abril de 2026; no localizada en PubMed.|Solo aprendizaje profundo; solo pacientes con escoliosis, por lo que no permite estimar detección; no analiza las condiciones técnicas de la imagen.|
|[CRD420251046877](https://www.crd.york.ac.uk/PROSPERO/view/CRD420251046877)|Guan y Zhao|Revisión sistemática de IA en tamizaje y diagnóstico de escoliosis de todos los tipos, incluidas la del adulto y la degenerativa, con apartados para diagnóstico en TC y en RM. Búsqueda de 2016 a febrero de 2025, solo en inglés; síntesis narrativa.|Declarada completada (versión 1.1, diciembre de 2025), pero no localizada en PubMed ni en Google Scholar (búsqueda por autores); los trabajos de esos autores que aparecen tratan de actividad física, rehabilitación digital y tamizaje escolar, no de IA en diagnóstico.|Alcance general sobre IA; no se restringe a adultos ni a RM y TC; no incluye métodos sin IA. La ficha indica, probablemente por error, que solo incluirá estudios aleatorizados.|
|[CRD420261476402](https://www.crd.york.ac.uk/PROSPERO/view/CRD420261476402)|Sun y Liu|Revisión sistemática de IA en toda la ruta clínica de la escoliosis (tamizaje, diagnóstico, predicción y tratamiento), en cualquier edad y etiología con Cobb mayor de 10°; prevé un análisis de subgrupos por modalidad. Búsqueda de 2016 a agosto de 2026, en inglés y chino.|En curso; fin previsto en agosto de 2027.|Solo pacientes con escoliosis diagnosticada; alcance general; no analiza las condiciones técnicas de la imagen.|

### Revisiones publicadas que se citarán como antecedentes

|Referencia|Tipo|Por qué no responde la pregunta de esta revisión|
|-|-|-|
|Zhu *et al.*, *Spine Deformity* 2024, [doi:10.1007/s43390-024-00954-4](https://doi.org/10.1007/s43390-024-00954-4)|Revisión sistemática y metaanálisis (PROSPERO CRD42023403057)|Limitada a radiografías.|
|Goldman *et al.*, *Spine Deformity* 2024, [doi:10.1007/s43390-024-00940-w](https://doi.org/10.1007/s43390-024-00940-w)|Revisión de alcance (JBI y PRISMA-ScR)|Limitada a menores de 18 años; casi todos los estudios incluidos usan radiografía.|
|Kumar *et al.*, *IEEE Access* 2024, [doi:10.1109/ACCESS.2024.3353794](https://doi.org/10.1109/ACCESS.2024.3353794)|Revisión sistemática declarada|Mezcla modalidades y edades; sin protocolo registrado ni evaluación de calidad; contiene errores de atribución de referencias, por lo que no se usarán sus datos.|
|Moung, Aishu y Farzamnia, *IJACSA* 16(9) 2025, [PDF](https://thesai.org/Downloads/Volume16No9/Paper_12-Automated_Scoliosis_Diagnosis_in_Spinal_Imaging.pdf)|Revisión de 55 estudios sobre diagnóstico automatizado de escoliosis|Mezcla modalidades (mayoría radiografía); no restringe por edad ni menciona protocolo registrado.|
|Jin *et al.*, *Sensors* 2022, [doi:10.3390/s22093258](https://doi.org/10.3390/s22093258)|Reseña narrativa|Métodos de medición del Cobb en varias modalidades, sin búsqueda sistemática.|
|Brigato *et al.*, *J Pediatr Orthop* 2026, [doi:10.1097/BPO.0000000000003451](https://doi.org/10.1097/BPO.0000000000003451)|Revisión sistemática|Topografía de superficie con aprendizaje automático en escoliosis idiopática; población pediátrica.|
|Avellanet *et al.*, *Front Med* 2026, [doi:10.3389/fmed.2026.1774697](https://doi.org/10.3389/fmed.2026.1774697)|Revisión rápida de revisiones sistemáticas|IA en escoliosis idiopática del adolescente.|

En conjunto, la evidencia de síntesis disponible se concentra en adolescentes y en radiografía. Las tres revisiones registradas que incluyen RM o TC en adultos lo hacen dentro de un alcance general, sin aislar esas modalidades ni analizar las condiciones técnicas de adquisición, que es el aporte específico de esta revisión de alcance.



## Declaración de uso de herramientas de IA

Se utilizaron herramientas de inteligencia artificial como apoyo durante la elaboración de este protocolo, principalmente para la construcción y revisión inicial de ecuaciones de búsqueda, la organización de ideas y el apoyo en la redacción del documento. Las estrategias de búsqueda, los resultados obtenidos y las decisiones metodológicas fueron revisados y corroborados manualmente por el autor. El contenido fue posteriormente modificado y ajustado de acuerdo con los objetivos y criterios definidos para esta revisión.

