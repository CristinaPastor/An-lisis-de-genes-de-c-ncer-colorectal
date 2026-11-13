ANÁLISIS DE GENES ASOCIADOS A FACTORES AMBIENTALES QUE AFECTAN AL CÁNCER COLORRECTAL
1. INTRODUCCIÓN: 

2. OBJETIVOS

3. ANÁLISIS 

3.1. FACTORES AMBIENTALES DE INTERÉS
Para comenzar, se debe seleccionar los distintos tipos de factores ambientales de interés que podrían estar involucrados en la enfermedad. Para ello, realizamos una búsqueda bibliográfica en PubMed y estudiamos qué factores poseen una alta relación con el cáncer de colon.
- Creamos una carpeta que se llame factores_ambientales.
- Dentro de la carpeta, clasificamos los diversos factores creando un archivo .md por cada factor.

3.2. SNPs RELACIONADOS CON LOS DISTINTOS FACTORES AMBIENTALES
Una vez seleccionado los factores ambientales de interés, es necesario establecer la relación o impacto de los mismos en la enfermedad. El estudio genético de enfermedades complejas y los factores ambientales se basa en los estudios de asociación del genoma completo (GWAS), Estos análisis evalúan millones  de polimorfismos de un solo nucleótido (SNPs) y requieren grandes muestras poblacionales, consorcios internacionales y repositorios públicos.

A partir de estos avances ha surgido la aleatorización mendeliana de dos muestras (2SMR), una metodología que emplea los SNPs como variables instrumentales (IVs) para inferir relaciones causales los factores de riesgo y la patología. 

A. Selección de los datos GWAS a analizar.
En primer lugar, se han seleccionado resultados públicos de GWAS tanto para las neoplasias digestivas como para los factores de riesgo de la base de datos de referencia para estudios de MR "ieu OpenGWAS". 

B. Análisis de MR.
Se ha realizado un estudio de 2SMR usando Rstudio con los paquetes "MR instruments" y "TwoSampleMR".
