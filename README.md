# ANÁLISIS DE GENES ASOCIADOS A FACTORES AMBIENTALES QUE AFECTAN AL CÁNCER COLORRECTAL
## 1. INTRODUCCIÓN

## 2. OBJETIVOS

## 3. ANÁLISIS 

### 3.1. FACTORES AMBIENTALES DE INTERÉS

Para comenzar, se debe seleccionar los distintos tipos de factores ambientales de interés que podrían estar involucrados en la enfermedad. Para ello, realizamos una búsqueda bibliográfica en PubMed y estudiamos qué factores poseen una alta relación con el cáncer de colon.
- Creamos una carpeta que se llame factores_ambientales.
- Dentro de la carpeta, clasificamos los diversos factores creando un archivo .md por cada factor.

### 3.2. SELECCIÓN DE SNPs Y ANÁLISIS DE ALEATORIZACIÓN MENDELIANA (MR).

Una vez seleccionado los factores ambientales de interés, es necesario establecer la relación o impacto de los mismos en la enfermedad. El estudio genético de enfermedades complejas y los factores ambientales se basa en los estudios de asociación del genoma completo (GWAS). Estos análisis evalúan millones  de polimorfismos de un solo nucleótido (SNPs) y requieren grandes muestras poblacionales, consorcios internacionales y repositorios públicos.

A partir de estos avances ha surgido la aleatorización mendeliana de dos muestras (2SMR), una metodología que emplea los SNPs como variables instrumentales (IVs) para inferir relaciones causales los factores de riesgo y la patología. 

#### A. Selección de los datos GWAS a analizar.
En primer lugar, los archivos "SNPs_relacionados_factoramiental.md" y "SNPs_relacionados_cancercolon.md" contienen la selección de resultados públicos de GWAS de interés para los factores de riesgo y para el cáncer de colon, respectivamente. Todo ello ha sido obtenido de la base de datos de referencia para estudios de MR "ieu OpenGWAS". 

#### B. Análisis de MR.
A continuación, se ha realizado un estudio de 2SMR usando Rstudio con los paquetes "MR instruments" y "TwoSampleMR".  
- En primer lugar se seleccionaron los SNPs asociados a cada factor ambiental para poder utilizarlos como IV.
- A continuación, se selecciona las IVs firmemente asociadas según el nivel de significación de GWAS.
- Se han empleado 5 métodos MR para los cuales se calculó el parámetro "beta", que refleja la dirección de la relación entre factor de riesgo/enfermedad.

En el archivo (Resultados_análisis_MR.md) se muestran los resultados obtenidos tras el análisis MR en función de sus 5 métodos,  mostrándose el factor de riesgo más significativo en cada método (p<0.05), el parámetro b y el nº de SNPs seleccionados para dicho factor.

### 3.3. ANÁLISIS DE SENSIBILIDAD

En este apartado se llevan a cabo los análisis estadísticos para confirmar la robustez de los resultados obtenidos. **El objetivo es descartar sesgos, factores de confusión y variantes con un peso desproporcionado en la relación causal analizada**.

#### 3.3.1 Análisis de Heterogeneidad
Mediante este análisis se evalúa si todos los SNPs contribuyen de forma similar al efecto observado sobre la enfermedad, o si hay algunos que tengan un peso notablemente mayor que otros.

Se pueden dar dos casos, cuya interpretación es:
- `p > 0.05` --> los **SNPs contribuyen de forma homogénea**, por lo que no hay heterogeneidad significativa.
- `p < 0.05` --> los **SNPs contribuyen de forma heterogénea**, de esta manera algunos SNPs tienen mayor influencia que otros.

#### 3.3.2 Análisis de Pleiotropía Horizontal
Se comprueba que la relación causal entre el factor de riesgo y la enfermedad es directa, sin que intervengan vías alternativas o factores de confusión.

Qué se interpreta:
- `p > 0.05` --> ausencia de pleiotropía horizontal: la relación causal es válida.
- `p < 0.05` --> posible pleiotropía: el modelo debe descartarse o revisarse.

> Se seleccionaron únicamente los modelos que no mostraron indicios de pleiotropía horizontal (`p > 0.05`).

#### 3.3.3 Análisis de SNPs Individuales (Single-SNP)
Mide el efecto de cada SNP de forma aislada mediante el test de Wald, observando si hay alguno que tenga especial influencia sobre el desarrollo de la enfermedad.

- `p < 0.05` --> el SNP tiene un efecto individual significativo y se considera candidato para explicar la base molecular del efecto observado.

#### 3.3.4 Análisis Leave-One-Out
Con este análisis se estudia el efecto del conjunto de SNPs excluyendo uno cada vez, pudiendo detectar si alguna variante condiciona por sí sola todo el resultado del análisis. Para ello, **si el valor de p pierde su significación estadística** tras la eliminación del SNP del conjunto, está **condicionando el efecto global** y habría que analizarlo con especial atención. 

#### 3.3.5 Análisis mediante representación gráfica 
Los resultados de estos análisis se representaron visualmente mediante cuatro tipos de gráficos.
Cada archivo de imagen corresponde a uno de los análisis descritos anteriormente.

- `single_snp_plot.png` --> representación del efecto individual de cada SNP
- `leave_one_out_plot.png` --> efecto del conjunto al excluir un SNP cada vez
- `scatter_plot.png` --> relación causal entre factor de riesgo y enfermedad
- `funnel_plot.png` --> simetría de los efectos pata detectar pleiotropía horizontal

