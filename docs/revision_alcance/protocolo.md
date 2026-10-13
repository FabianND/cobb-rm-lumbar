# Protocolo de la revisión de alcance

**Título propuesto:** Medición automática y semiautomática de la curvatura coronal de la columna y detección de escoliosis en resonancia magnética y tomografía computarizada de adultos: protocolo de revisión de alcance.



**Documento relacionado:** [`pcc\_y\_busqueda\_de\_registros.md`](pcc_y_busqueda_de_registros.md), con la pregunta, los criterios PCC y la búsqueda de revisiones existentes.

La estructura sigue los bloques de la plantilla *Generalized Systematic Review Registration* de OSF (van den Akker *et al.*, *Systematic Reviews* 2023; doi:[10.1186/s13643-023-02281-7](https://doi.org/10.1186/s13643-023-02281-7)) para que el registro consista en trasladar cada sección a su campo correspondiente. La conducción y el reporte seguirán el manual de JBI para revisiones de alcance y la lista PRISMA-ScR (Tricco *et al.*, *Ann Intern Med* 2018; doi:[10.7326/M18-0850](https://doi.org/10.7326/M18-0850)).

\---

## 1\. Datos generales

|Campo|Contenido|
|-|-|
|Tipo de revisión|Revisión de alcance (*scoping review*).|
|Autor y roles|Edwar Fabian Nossa Díaz, programa de Ingeniería Biomédica de la Escuela Colombiana de Ingeniería Julio Garavito y la Universidad del Rosario: concepción, búsqueda, cribado, extracción, síntesis y redacción.|
|Etapa al registrar|Pregunta y criterios definidos; búsqueda de revisiones existentes completada (3-oct-2026); estrategia de PubMed definida y piloteada (8-oct-2026); cribado no iniciado.|
|Fechas|Inicio: noviembre de 2026. Fin: mayo de 2027.|
|Financiamiento|Sin financiamiento específico.|
|Conflictos de interés|Ninguno declarado.|
|Uso de herramientas de IA|Se utilizaron herramientas de inteligencia artificial como apoyo durante la elaboración de este protocolo, principalmente para la construcción y revisión inicial de ecuaciones de búsqueda. Las búsquedas reportadas, las decisiones de elegibilidad y la extracción las realiza y verifica el autor. Cualquier uso adicional (por ejemplo, conteo de duplicados) se declarará en el informe final.|

## 2\. Antecedentes y preguntas

### Antecedentes

La escoliosis del adulto se diagnostica y gradúa con el ángulo de Cobb medido en radiografía de pie. Sin embargo, una parte importante de los adultos se realiza RM o TC de columna o de abdomen por otros motivos, y en esos estudios la curvatura coronal también es visible, aunque en decúbito. Los métodos automáticos podrían aprovechar esas imágenes para medir la curvatura o detectar escoliosis de forma oportunista. Las revisiones disponibles se concentran en radiografía y en población adolescente, y las tres revisiones registradas que incluyen RM o TC en adultos lo hacen dentro de un alcance general, sin aislar esas modalidades ni analizar el estándar de referencia ni las condiciones técnicas de adquisición (ver la sección 4 del documento PCC). Esta revisión busca mapear esa evidencia.

### Pregunta principal

> ¿Qué métodos automáticos o semiautomáticos se han publicado para medir la curvatura coronal de la columna (ángulo de Cobb u otra medida angular o geométrica explícita) o para detectar escoliosis en resonancia magnética o tomografía computarizada de adultos, frente a qué estándar de referencia se han validado (quién midió, sobre qué imagen y en qué posición del paciente) y qué características de las imágenes se han estudiado como fuente de variación?

### Subpreguntas

1. ¿Qué modalidades de imagen, secuencias, regiones de la columna y contextos clínicos se han utilizado en los estudios incluidos?
2. ¿Qué objetivos persiguen los métodos (medición del ángulo de Cobb, medición de otras características explícitas de la curvatura, detección o clasificación de escoliosis) y qué grado de intervención manual requieren?
3. ¿Qué estándares de referencia se han utilizado para validar los métodos, quién realizó las mediciones, sobre qué imágenes y en qué posición se encontraba el paciente? ¿Qué métricas se emplearon para evaluar el desempeño y la concordancia?
4. ¿Qué características técnicas de las imágenes (grosor de corte, resolución espacial, secuencia, equipo y centro) se reportan y cuáles se han evaluado como fuentes de variación del desempeño?
5. ¿Con qué frecuencia se reportan validaciones externas y qué disponibilidad tienen el código, los datos y otros recursos necesarios para reproducir los métodos?

La cuarta subpregunta tiene un propósito de mapeo: describir qué se ha reportado, y qué no, sobre la influencia de las características técnicas en el desempeño de los métodos. La revisión no evaluará por sí misma la calidad de las imágenes de los estudios incluidos.

### Hipótesis

No aplica: es una revisión de alcance descriptiva y no pone a prueba hipótesis.

## 3\. Estrategia de búsqueda

### Bases e interfaces

|Base|Interfaz|Estado|
|-|-|-|
|MEDLINE|PubMed (web)|Estrategia definitiva (versión B) piloteada el 8-oct-2026: 656 registros; recupera los 6 estudios de validación.|
|Scopus|Scopus (web, acceso institucional)|Piloteada el 9-oct-2026: 1.209 registros; recupera los 6 estudios de validación.|
|IEEE Xplore|IEEE Xplore, *Command Search*|Piloteada el 9-oct-2026: 332 registros. Ninguno de los estudios de validación está publicado en revistas o congresos de IEEE, por lo que no aplica la verificación.|

Embase y Web of Science Core Collection no se consultarán porque las cuentas institucionales del autor no tienen acceso a ellas, lo que se reportará como limitación. Para mitigarla, la búsqueda en bases se complementa con la revisión de referencias y citas de los estudios incluidos (ver "Otras fuentes").

### Estrategia de PubMed (versión B, definitiva)

```text
#1  "Scoliosis"\[Mesh] OR scolio\*\[tiab] OR Cobb\[tiab] OR "lateral curvature\*"\[tiab]
    OR "spinal curvature\*"\[tiab] OR (("coronal curvature\*"\[tiab] OR "coronal deformit\*"\[tiab]
    OR "coronal alignment"\[tiab]) AND (spine\[tiab] OR spinal\[tiab] OR vertebra\*\[tiab]
    OR lumbar\[tiab] OR thoracic\[tiab]))

#2  "Artificial Intelligence"\[Mesh] OR "Pattern Recognition, Automated"\[Mesh]
    OR "Image Processing, Computer-Assisted"\[Mesh:NoExp] OR automat\*\[tiab] OR semiautomat\*\[tiab]
    OR "semi-automat\*"\[tiab] OR "deep learning"\[tiab] OR "machine learning"\[tiab]
    OR "artificial intelligence"\[tiab] OR "neural network\*"\[tiab] OR convolutional\[tiab]
    OR "computer-aided"\[tiab] OR "computer-assisted"\[tiab] OR computeri\*\[tiab]
    OR segmentation\[tiab] OR algorithm\*\[tiab] OR software\[tiab] OR computational\[tiab]
    OR "image analysis"\[tiab] OR "image processing"\[tiab] OR matlab\[tiab] OR program\*\[tiab]
    OR centroid\*\[tiab] OR spline\*\[tiab] OR "curve fitting"\[tiab]

#3  "Magnetic Resonance Imaging"\[Mesh] OR "Tomography, X-Ray Computed"\[Mesh] OR MRI\[tiab]
    OR "magnetic resonance"\[tiab] OR "MR imaging"\[tiab] OR "computed tomography"\[tiab]
    OR CT\[tiab]

#4  #1 AND #2 AND #3 NOT ("Animals"\[Mesh] NOT "Humans"\[Mesh])
```

No se aplican filtros de edad, idioma ni fecha en la búsqueda, porque los filtros de edad dependen de la indexación y harían perder estudios con población mixta. La población y el idioma se evalúan en el cribado.

### Desarrollo de la estrategia de PubMed

La estrategia se refinó el 8-oct-2026 a partir de un piloto. La versión inicial (A) usaba en el bloque de automatización los MeSH expandidos "Image Processing, Computer-Assisted" e "Image Interpretation, Computer-Assisted" y devolvió 2.011 registros. Al analizar la exportación con sus MeSH, 1.702 registros no contenían ningún término de automatización en el título, el resumen ni las palabras clave, y 1.209 de los que tampoco tenían un MeSH de automatización estaban indexados con "Tomography, X-Ray Computed". Es decir, con esos MeSH expandidos el bloque de automatización se cumplía por el solo hecho de que el estudio fuera una TC. Además, los términos "coronal alignment" y afines recuperaban estudios de rodilla y tobillo sin relación con la columna.

La versión definitiva (B) reemplaza esos MeSH por "Artificial Intelligence" y "Pattern Recognition, Automated" expandidos y por "Image Processing, Computer-Assisted" sin expandir; amplía los términos de texto (computeri\*, algorithm\*, software, computational, image analysis/processing); añade términos para métodos computacionales descritos sin vocabulario de automatización (matlab, program\*, centroid\*, spline\*, curve fitting), y exige que los términos coronales aparezcan junto a un término de columna. Los términos computacionales se añadieron porque un estudio probablemente elegible (Cobb estimado con programas propios en MATLAB sobre TC lumbar de adultos; PMID 37737438) solo era recuperado por el MeSH "Imaging, Three-Dimensional", cuya inclusión habría añadido 176 registros mayoritariamente quirúrgicos.

|Versión|Registros en PubMed|Estudios de validación recuperados|
|-|-|-|
|A (inicial)|2.011|6 de 6|
|B (definitiva)|656|6 de 6|

### Ecuaciones para las demás bases

Las ecuaciones se tradujeron sin vocabulario controlado. En Scopus el bloque de automatización se limita a título, resumen y palabras clave de autor, porque sus campos de indexación pueden contener expresiones como "computer assisted tomography" que reproducirían el problema descrito para la versión A. En IEEE Xplore se omite el bloque de automatización, porque su contenido es predominantemente técnico y sus términos de indexación (INSPEC) incluyen "computerised tomography" en los estudios de TC.

**Scopus (búsqueda avanzada)**

```text
TITLE-ABS-KEY ( scolio\* OR cobb OR "lateral curvature\*" OR "spinal curvature\*"
  OR ( ( "coronal curvature\*" OR "coronal deformit\*" OR "coronal alignment" )
  AND ( spine OR spinal OR vertebra\* OR lumbar OR thoracic ) ) )
AND ( TITLE-ABS ( automat\* OR semiautomat\* OR "semi-automat\*" OR "deep learning"
  OR "machine learning" OR "artificial intelligence" OR "neural network\*" OR convolutional
  OR "computer-aided" OR "computer-assisted" OR computeri\* OR segmentation OR algorithm\*
  OR software OR computational OR "image analysis" OR "image processing" OR matlab
  OR program\* OR centroid\* OR spline\* OR "curve fitting" OR "pattern recognition" )
  OR AUTHKEY ( automat\* OR semiautomat\* OR "deep learning" OR "machine learning"
  OR "artificial intelligence" OR "neural network\*" OR convolutional OR segmentation
  OR algorithm\* OR "pattern recognition" ) )
AND TITLE-ABS-KEY ( mri OR "magnetic resonance" OR "MR imaging" OR "computed tomography"
  OR ct OR tomograph\* )
```

**IEEE Xplore (Command Search)**

```text
("All Metadata":scoliosis OR "All Metadata":scoliotic OR "All Metadata":"Cobb angle"
  OR "All Metadata":"spinal curvature" OR "All Metadata":"spine curvature")
AND ("All Metadata":MRI OR "All Metadata":"magnetic resonance" OR "All Metadata":"computed tomography"
  OR "All Metadata":CT)
```

Si alguna interfaz rechaza la ecuación por longitud o número de comodines, se dividirá el bloque de automatización en dos búsquedas, se exportarán ambas y los duplicados se eliminarán en Rayyan; la división se reportará.

### Validación de la búsqueda

La estrategia se considera aceptable si recupera, en cada base donde estén indexados, los siguientes estudios identificados de antemano como probablemente elegibles. En Scopus la verificación se hace combinando la ecuación con los DOI.

|Estudio|Modalidad|PMID|DOI|
|-|-|-|-|
|van der Graaf *et al.*, *Eur Radiol* 2024|RM lumbar sagital|38383922|[10.1007/s00330-024-10616-8](https://doi.org/10.1007/s00330-024-10616-8)|
|Niglas *et al.*, *Eur Spine J* 2026|RM Dixon abdominal|42606698|[10.1007/s00586-026-10239-1](https://doi.org/10.1007/s00586-026-10239-1)|
|Alukaev *et al.*, *Eur Spine J* 2022|TC|35596800|[10.1007/s00586-022-07245-4](https://doi.org/10.1007/s00586-022-07245-4)|
|Li *et al.*, *J Imaging Inform Med* 2024|TC|39117939|[10.1007/s10278-024-01211-w](https://doi.org/10.1007/s10278-024-01211-w)|
|Bonanni, *Int J Spine Surg* 2017|RM|28765806|[10.14444/4022](https://doi.org/10.14444/4022)|
|Arginteanu *et al.*, *Spine Deform* 2024|TC|37737438|[10.1007/s43390-023-00752-4](https://doi.org/10.1007/s43390-023-00752-4)|

Si alguno no aparece en una base donde está indexado, se revisará qué término no está cubierto y se ajustará la ecuación antes de la búsqueda definitiva. Los cambios se documentarán.

### Otras fuentes

Se revisarán las listas de referencias de los estudios incluidos y de las revisiones relacionadas identificadas en el documento PCC (búsqueda hacia atrás), y los trabajos que citan a los estudios incluidos mediante Google Scholar (búsqueda hacia adelante). Las tesis y los preprints que aparezcan solo se usarán como fuentes de apoyo, de acuerdo con los criterios de elegibilidad. No se contactará a los autores.

### Fecha y repetición

Las búsquedas definitivas se ejecutarán en un mismo periodo de una semana y se reportará la fecha de cada una. Si entre la búsqueda y el envío del manuscrito pasan más de seis meses, se repetirá con la misma estrategia, limitada a las fechas posteriores.

## 4\. Cribado

### Herramientas y gestión de registros

Los resultados de cada base se exportarán en formato RIS o CSV y se importarán en Rayyan, donde se eliminarán duplicados con la detección automática y una revisión manual de los casos dudosos. Se registrará el número de registros por base, de duplicados eliminados y de registros cribados, para el diagrama de flujo PRISMA-ScR.

### Etapas

El cribado tendrá dos etapas: primero títulos y resúmenes, y después texto completo. En la primera etapa, cualquier registro con información insuficiente o dudosa pasa a texto completo en lugar de excluirse. En la segunda se registrará un único motivo de exclusión por estudio, siguiendo el orden de los criterios.

### Criterios aplicados en orden

1. Es un estudio primario (no revisión, editorial, carta ni resumen de congreso sin texto completo).
2. Incluye personas vivas (se excluyen cadáveres, fantomas y estudios solo con animales).
3. La población es adulta (≥ 18 años), o los resultados de adultos se reportan por separado o pueden extraerse.
4. Usa RM o TC, de cualquier región de la columna. Se incluye la TC de haz cónico, incluida la adquirida en bipedestación, porque permite comparar la medición en carga con la realizada en decúbito; en la extracción se registra por separado de la TC multicorte.
5. El método es automático o semiautomático.
6. El método mide el Cobb coronal u otra medida explícita de curvatura coronal, o detecta o clasifica escoliosis. Los métodos que solo segmentan o localizan se incluyen únicamente si forman parte de un procedimiento destinado a detectar o medir la curvatura. Las medidas exclusivamente sagitales (cifosis, lordosis) no cumplen este criterio; las medidas tridimensionales se incluyen si reportan o permiten derivar un componente coronal.
7. Es un artículo de revista revisada por pares o un artículo completo de congreso.
8. Está en inglés o español.

### Revisor único y consistencia

El cribado lo realizará un único revisor (el autor), lo cual se declarará como limitación, dado que JBI recomienda dos revisores independientes. Para medir la consistencia, el autor volverá a cribar una muestra aleatoria del 20 % de los títulos y resúmenes al menos dos semanas después de la primera decisión, sin ver las decisiones anteriores, y se reportará la concordancia intraevaluador con kappa de Cohen. Antes del cribado completo se hará una prueba piloto con 50 registros al azar para afinar la interpretación de los criterios, y los ajustes que resulten se documentarán. Si más adelante se incorpora un segundo revisor, el cambio se registrará como enmienda en OSF.

## 5\. Extracción de datos

### Formulario

La extracción se hará en una hoja de cálculo con una fila por estudio y las variables definidas en la tabla siguiente. Cuando un estudio reporte varios métodos o conjuntos de prueba, se extraerá una fila por combinación de método y conjunto de prueba.

|Grupo|Variables|
|-|-|
|Identificación|Autor, año, país, revista o congreso, DOI.|
|Población|Tamaño de muestra, edad (media o rango), proporción de mujeres, diagnóstico o motivo del estudio, número de centros, si es población mixta y cómo se separaron los adultos.|
|Imagen|Modalidad; región de la columna; secuencia o protocolo; plano adquirido (sagital, coronal, axial, 3D); resolución en el plano; grosor de corte; fabricante y campo magnético, o tipo de TC (multicorte o de haz cónico); posición del paciente (decúbito o bipedestación); contexto (estudio dirigido a la columna u oportunista).|
|Método|Objetivo (detección de escoliosis, clasificación, medición del Cobb, otra medida de curvatura, segmentación o localización como paso intermedio); enfoque (segmentación, puntos de referencia, regresión directa, otro); grado de automatización (automático o semiautomático, y qué paso es manual); definición operativa del ángulo o de la medida.|
|Estándar de referencia|Quién midió (profesión, experiencia, número de lectores), sobre qué imagen (radiografía de pie, la misma RM o TC, otra) y en qué posición; si se reportó la variabilidad entre lectores.|
|Desempeño|Métricas reportadas (MAE, ICC y su tipo, Bland-Altman, correlación, sensibilidad, especificidad, AUC) con sus valores e intervalos de confianza cuando existan; umbral usado para definir escoliosis.|
|Validación y fuentes de variación|Tipo de validación (interna, externa, temporal); características técnicas analizadas como fuente de variación y su resultado.|
|Reproducibilidad|Disponibilidad de código, de modelo entrenado y de datos.|

### Procedimiento

El formulario se pilotará con cinco estudios incluidos y se ajustará antes de la extracción completa. El autor extraerá todos los estudios. Los datos ausentes se registrarán como "no reportado" y no se imputarán.

## 6\. Síntesis

Los resultados se presentarán de forma descriptiva, sin metaanálisis, porque el objetivo es mapear la evidencia y no estimar un efecto conjunto. Se reportará el diagrama de flujo PRISMA-ScR; tablas de características de los estudios; y conteos y tablas cruzadas por modalidad, región, contexto, objetivo del método, grado de automatización, tipo de estándar de referencia y posición del paciente en la referencia. Las métricas de desempeño se tabularán tal como fueron reportadas, sin combinarlas, señalando cuándo provienen de validación interna o externa. Se acompañará con un resumen narrativo que identifique vacíos de evidencia; en particular, la frecuencia de validación contra radiografía de pie, la de validación externa y la de análisis de las condiciones técnicas.

No se evaluará la calidad metodológica ni el riesgo de sesgo de los estudios incluidos, de acuerdo con la guía de JBI para revisiones de alcance. En su lugar, se describirán características de diseño relevantes para interpretar la evidencia, como el tipo de validación, el tamaño de la muestra de prueba y la naturaleza del estándar de referencia.

## 7\. Datos y materiales

Las cadenas de búsqueda, las exportaciones de cada base (solo metadatos bibliográficos), las decisiones de cribado exportadas de Rayyan y la hoja de extracción se publicarán en este repositorio y se enlazarán desde el registro de OSF. No se publicarán textos completos de artículos.

## 8\. Enmiendas

Toda desviación respecto de este protocolo se registrará en OSF con fecha y justificación, y se reportará en el manuscrito final.

