# Sistema de distribución de potencia en Colombia  
## Introducción
Para Enel Colombia la calidad de servicio es un tema de vital importancia, de tal manera que se encuentra declarada en su Política Integrada de Salud & Seguridad Laboral, Medio Ambiente, Calidad y Energía y hace énfasis en su eje estratégico organizacional denominado Competitividad, “entendida en términos de Excelencia Operacional, traducida en excelencia en la calidad y la atención al cliente, excelencia técnica en todas las actividades y funciones que adelantan (disponibilidad, calidad del servicio y control de pérdidas), logrando operar de forma óptima el negocio para convertirse en líderes frente a sus competidores” . De esta manera para Enel Colombia es importante mantener la continuidad del servicio y disminuir la tasa de fallas y la duración de estas. 

 
El presente trabajo aborda el desarrollo de un modelo para establecer las acciones que requiere el operador de red Enel Colombia en su sistema de distribución, minimizando los indicadores de continuidad del suministro eléctrico mediante mantenimientos correctivos, trabajos de inversión o reconfiguraciones de la topología del circuito. La determinación de los circuitos a incluir en el plan de mantenimiento y los trabajos a realizar es crucial para la optimización ya que siempre se busca mejora en la confiabilidad del sistema; lo que se pretende es analizar la información de la composición eléctrica  del circuito, causas de falla e indicadores de calidad para luego presentar una metodología y la elaboración de un modelo que clasifique los circuitos eléctricos de media tensión en las diferentes actividades que se deban realizar y poder finalmente exponer recomendaciones al operador de red, de las ventajas y/o desventajas de implementar el modelo propuesto. 

## Descripción de un sistema de distribución

Se entiende por sistema de distribución de energía eléctrica a la disposición adoptada por los elementos del sistema tales cómo conductores, transformadores y protecciones, con el fin de lograr que la energía generada por las centrales eléctricas y transportada a través del sistema de transmisión o inmersa en el sistema de distribución, pueda ser utilizada en los sitios de consumo, o sea la carga (residencial, comercial e industrial). Los transformadores de distribución están conectados por el primario al sistema de Media Tensión y por el secundario a la red de Baja Tensión, llevando la potencia a niveles de utilización para los usuarios conectados. 
![Image](docs/figures/sistema_distribucion.png)


## Estructura del repositorio

├── LICENSE  
├── README.md          <- README para los desarrolladores.  
├── data  
│   ├── external       <- Datos desde teceras partes.  
│   ├── interim        <- Data intermedia que ha sido transformada  
│   ├── processed      <- Data canonical final lista para los modelos  
│   └── raw            <- Original e inmutable data.  
├── docs               <- documentación creada.  
├── models             <- Resumen de modelos.  
├── reports            <- Análisis generados como HTML, PDF, LaTeX, etc.  
│   └── figures        <- Figures generadas para sr usadas en reporting.  
│
├── requirements.txt   <- requerimientos.txt para crear el ambiente de desarollo con `pip freeze > │                        requirements.txt`  
│
├── src                <- Código fuente para este proyecto.  
│   └── notebooks  <- notebooks de jupyter  
│

## Selección de circuitos

### Iteración 0:
Una preliminar análisis exploratorio de datos puede ser encontrado [aquí.](src/notebooks/Iteraction_0/1_0_exploracion_inicial_datos_Iteracion_0.ipynb) . Este analisis preliminar fue corrido con el dataset original, encontrado [aquí.] (data/raw/dataset_pfinal_ANS.xls)

- Estadisticas descriptivas pueden ser consultadas [aquí.](reports/figures)

### Iteración 1: 
Un nuevo dataset fue suministrado con datos de campo corregidos por que hubo muchos circuitos con NaN y la conclusion fue que esos circuitos fueron dados de baja. [detalles](data/raw/dataset_pfinal_ANS_V2.xlsx) 

- Con estas nuevos ajustes del dataset original, se hizo  de nuevo exploración de datos cuyas figuras se encuentra [aquí](/docs/figures/Iteracion_1)

- En esta iteración se corrió PCA con el animo de ver si la reducción de dimensionalidad nos proporciona una reducción significativa. Al 95% de varianza explicada solamente se reduce el 50% de dimensionalidad. Creemos que que esta reduccion no es suficiente y se decide continuar sin PCA. En el repositorio se puede encontrar las figuras resultantes de Varianza explicada, dendrogramas, Varianza Intracluster, Indices de Silhoutte, dbscan kneelocator, dbscan-porcentaje de Outliers [aquí.](/docs/figures/Iteracion_1)

- En esta Iteración se corre Clustering jerárquico para obtener una referencia del numero de clusters y volvemos a aplicar KMeans. Los notebooks resultantes se encuetnran [aquí.](src/notebooks/Iteracion_1)

### Iteración 2: 

- Un nuevo dataset fue suministrado con algunos datos de campo corregidos de nivel de tension en  algunos circuitos [Ver](data/raw/dataset_pfinal_ANS_V4.xlsx) 

-  En esta Iteración se corre Clustering jerárquico para obtener una referencia del numero de clusters y volvemos a aplicar KMeans. Los notebooks resultantes se encuentran [aquí.](src/notebooks/Iteracion_2)

### Iteración 3: 

- Un nuevo dataset fue suministrado desde el centro de operaciones de la compania , las cuales les fueron eliminados algunas columnas por ser redundantes y con la modificación de tener solamente  la Unidad Territorial V (Metropolitana Noroccidente) que abarca los circuitos de  la localidad de Suba y los municipios de Chía, Cota, Cajicá Tenjo y Tabio y con algunos datos de campo corregidos de nivel de tensión en  algunos circuitos [detalles](data/raw/dataset_pfinal_ANS_V6.xlsx) 

- A partir de este dataset , se aplica Clustering Jerarquico para retener 12 clusters que corresponden a los doce meses dentro del plan de mantenimiento. Aqui se ordenan los clusters por mayor saidi y de cada cluster se toma el 40% de circuitos que  les será aplicado el plan de mantenimiento.[ver notebook](src/notebooks/Iteracion_3/7_0_Clustering_Jerarquico__Iteration_3.ipynb). La seleccion de los circuitos se pueden encontrar [aquí.](data/processed/pca_cluster_jerarquico/circuits_selection)


- A partir 

## Clonar repositorio
Usando git o otra herramienta de control de versiones como sourcetree or github desktop, clonar este repositorio desde esta URL:
https://github.com/EduardoToledoMIAD/distribucion_potencia.git