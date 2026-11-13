ANÁLISIS DE GENES ASOCIADOS A FACTORES AMBIENTALES QUE AFECTAN AL CÁNCER COLORRECTAL
1. INTRODUCCIÓN: 

2. OBJETIVOS

3. ANÁLISIS 

3.1. FACTORES AMBIENTALES DE INTERÉS

Para comenzar, se debe seleccionar los distintos tipos de factores ambientales de interés que podrían estar involucrados en la enfermedad. Para ello, realizamos una búsqueda bibliográfica en PubMed y estudiamos qué factores poseen una alta relación con el cáncer de colon.
- Creamos una carpeta que se llame factores_ambientales.
- Dentro de la carpeta, clasificamos los diversos factores creando un archivo .md por cada factor.

3.2. SELECCIÓN DE SNPs Y ANÁLISIS DE ALEATORIZACIÓN MENDELIANA (MR).

Una vez seleccionado los factores ambientales de interés, es necesario establecer la relación o impacto de los mismos en la enfermedad. El estudio genético de enfermedades complejas y los factores ambientales se basa en los estudios de asociación del genoma completo (GWAS), Estos análisis evalúan millones  de polimorfismos de un solo nucleótido (SNPs) y requieren grandes muestras poblacionales, consorcios internacionales y repositorios públicos.

A partir de estos avances ha surgido la aleatorización mendeliana de dos muestras (2SMR), una metodología que emplea los SNPs como variables instrumentales (IVs) para inferir relaciones causales los factores de riesgo y la patología. 

A. Selección de los datos GWAS a analizar.
En primer lugar, los archivos "SNPs_relacionados_factoramiental.md" y "SNPs_relacionados_cancercolon.md" contienen la selección de resultados públicos de GWAS de interés para los factores de riesgo y para el cáncer de colon, respectivamente. Todo ello ha sido obtenido de la base de datos de referencia para estudios de MR "ieu OpenGWAS". 

B. Análisis de MR.
A continuación, se ha realizado un estudio de 2SMR usando Rstudio con los paquetes "MR instruments" y "TwoSampleMR".  
- En primer lugar se seleccionaron los SNPs asociados a cada factor ambiental para poder utilizarlos como IV.
- A continuación, se selecciona las IVs firmemente asociadas según el nivel de significación de GWAS.
- Se han empleado 5 métodos MR para los cuales se calculó el parámetro "beta", que refleja la dirección de la relación entre factor de riesgo/enfermedad.

En el archivo (Resultados_análisis_MR.md) se muestran los resultados obtenidos tras el análisis MR en función de sus 5 métodos,  mostrándose el factor de riesgo más significativo en cada método (p<0.05), el parámetro b y el nº de SNPs seleccionados para dicho factor.

3.3. 
