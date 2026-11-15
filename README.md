# ANÁLISIS DE GENES ASOCIADOS A FACTORES AMBIENTALES QUE AFECTAN AL CÁNCER COLORRECTAL

## 1. INTRODUCCIÓN

Los cánceres se clasifican como enfermedades complejas debido a que su aparición depende tanto de factores genéticos como de la interacción de estos con factores ambientales. Actualmente, se atribuye a las modificaciones epigenéticas el papel de mediar diálogo entre la genética y el ambiente. Existe un gran abanico de factores ambientales asociados a enfermedades y en nuestro caso, seleccionamos a las neoplasias digestivas como principal objetivo de estudio. 

La base del estudio de las bases genéticas de las enfermedades complejas y de los factores ambientales se fundamenta en estudios de asociación del genoma completo (GWAS del inglés, Genome-wide association studies) que consiste en el análisis de millones de polimorfismos de un solo nucleótido (SNPs del inglés, Single Nucleotide Polymorphism) que se encuentran localizados a lo largo del genoma, y su asociación con las diferentes neoplasias. Además, gracias a las grandes iniciativas internacionales y consorcios, se han podido desarrollar unos métodos conocidos como aleatorización mendeliana de dos muestras (2SMR del inglés, Two-sample mendelian randomization) donde utilizamos los SNPs como variables instrumentales, con la finalidad de comprobar la existencia de una relación causal entre factor ambiental y neoplasia digestiva. 

Este proyecto de investigación se basa, por tanto, en el estudio de factores ambientales que puedan influir en el desarrollo de neoplasias digestivas, en nuestro caso el cáncer de colon, mediante estudios de asociación de genoma completo y aplicación del método de aleatorización mendeliana de dos muestras a través del lenguaje de programación R en la plataforma de R studio. 

## 2. OBJETIVOS

Planteamos los siguientes objetivos:
* Evaluar el efecto causal de los factores ambientales sobre el cáncer de colon mediante el uso de herramientas de aleatorización mendeliana de dos muestras (2SMR).
* Determinar la solidez de las asociaciones causales empleando análisis de sensibilidad.
* Explorar el papel de los SNPs como variables instrumentales (IVs) para profundizar en la comprensión de las bases moleculares de las relaciones causales.

## 3. ANÁLISIS 

### 3.1. FACTORES AMBIENTALES DE INTERÉS

Para comenzar, se debe seleccionar los distintos tipos de factores ambientales de interés que podrían estar involucrados en la enfermedad. Para ello, realizamos una búsqueda bibliográfica en PubMed y estudiamos qué factores poseen una alta relación con el cáncer de colon.
- Creamos una carpeta que se llame factores_ambientales.
- Dentro de la carpeta, clasificamos los diversos factores creando un archivo .md por cada factor.
- En cada archivo recopilamos toda la bibliografía inicial de apoyo con la que podremos tener una primera idea de qué factores tienen más probabilidad de participar en la enfermedad. 

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

### 3.4. Análisis funcional de las variantes genéticas

En esta sección se estudian las posibles consecuencias funcionales de las variantes genéticas identificadas en los análisis previos, prestando especial atención a los genes relacionados y a sus posibles efectos sobre la expresión génica y los procesos de regulación biológica.

El análisis incluye:
- Identificación de los genes relacionados con las variantes genéticas seleccionadas.
- Consulta de posibles efectos funcionales, como los efectos eQTL.
- Interpretación biológica de la información disponible.
- Recopilación de recursos y herramientas bioinformáticas para la anotación funcional.

Las tres variantes documentadas en esta sección proceden del análisis de cáncer de colon. Se consideran datos de referencia bibliográfica

**Archivos relacionados:**
- `analisis_funcional/analisis_funcional.md` --> descripción del enfoque y los objetivos.
- `analisis_funcional/tabla_variantes.csv` --> tabla de variantes y genes relacionados.
- `analisis_funcional/recursos_analisis_funcional.md` --> recursos y herramientas de consulta.

### 3.5. Genes funcionales relacionados con la patología

En esta sección se recopilan los genes identificados durante el análisis funcional de las variantes genéticas asociadas a factores antropométricos relacionados con neoplasias digestivas.

El objetivo de este apartado es proporcionar una interpretación biológica de los resultados obtenidos mediante los análisis de Randomización Mendeliana, identificando genes candidatos que podrían participar en los mecanismos moleculares implicados en el desarrollo tumoral.

El análisis incluye:

- Identificación de genes asociados a las variantes genéticas de interés.
- Descripción de la función biológica conocida de cada gen.
- Revisión de la evidencia disponible sobre su posible implicación en la enfermedad.
- Clasificación de los genes según la patología con la que fueron asociados.
  
Los genes se han organizado en función de la patología estudiada:

- **Cáncer colorrectal**.
- **Cáncer de hígado**.
Cada gen dispone de una ficha individual que incluye una descripción resumida de su función biológica y de su posible papel en los procesos relacionados con la carcinogénesis.

Archivos relacionados:

- genes_funcionales/cancer_colorrectal/ --> genes asociados al cáncer colorrectal.
- genes_funcionales/cancer_higado/ --> genes asociados al cáncer de hígado.

## 4.CONCLUSIONES
Los análisis realizados permitieron identificar factores antropométricos y ambientales potencialmente relacionados con el riesgo de desarrollar cáncer colorrectal mediante estrategias de Randomización Mendeliana basadas en datos GWAS públicos.

Los resultados obtenidos fueron evaluados mediante distintos análisis de sensibilidad con el objetivo de confirmar la robustez de las asociaciones observadas y reducir la influencia de posibles factores de confusión o sesgos metodológicos.

Además, la caracterización funcional de las variantes genéticas permitió identificar genes candidatos susceptibles de participar en los mecanismos biológicos implicados en la enfermedad. El estudio de estos genes aporta información complementaria para interpretar los resultados desde una perspectiva molecular y facilita la identificación de posibles rutas biológicas involucradas en la carcinogénesis.

En conjunto, este trabajo demuestra la utilidad de integrar datos genéticos, análisis de causalidad y herramientas de anotación funcional para mejorar la comprensión de los factores relacionados con el desarrollo de neoplasias digestivas.

### AUTORES

Denia Hassan Mohamed

Elisa Palos Domínguez

Carmen Galiano Gamez

Damián Tandalla Guacollantes

Cristina Pastor López
