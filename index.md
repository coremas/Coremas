## Portafolio de proyectos Sebastián Vargas.

### COVID-19 en León, Guanajuato. Expresión cartográfica del Índice de Riesgo de Contagio Interurbano e Intergeneracional (IRCII).
#### En colaboración con el Dr. José Luis Coronado Ramírez y el Dr. Ernesto Cervantes López.

Instrumento de carácter cuantitativo y [*traducido en cartografía web interactiva*](https://www.routledge.com/Web-Cartography-Map-Design-for-Interactive-and-Mobile-Devices/Muehlenhaus/p/book/9781439876220) que tuvo por finalidad identificar zonas con diferente intensidad de riesgo de contagio para la ciudad de León, Guanajuato, en el marco de la pandemia global de COVID-19, provocada por el virus SARS-COV2. Dicho instrumento, en forma de [*índice compuesto*](https://stats.oecd.org/glossary/detail.asp?ID=6278), se construyó a partir de la combinación de diferentes factores de [*riesgo*](https://www.redalyc.org/articulo.oa?id=73111844003), tales como:

1) las oportunidades de movilidad en transporte público, 
2) la disponibilidad y concentración de establecimientos esenciales, 
3) la interacción entre diferentes grupos etarios, 
4) la densidad poblacional, y 
5) la disponibilidad de agua entubada. 
 
Partiendo de que el riesgo es omnipresente, la cartografía de este índice permite distinguir diferentes zonas de la ciudad en función de su grado de riesgo de contagio.

El mapa interactivo está disponible [aquí](https://coremas.github.io/IRCII/). Al deslizar el cursor por el mapa, se ilumina e identifica la colonia señalada por el cursor, permitiendo notar si ésta se encuentra en una zona de muy alto riego (zonas oscuras) o de riesgo bajo (zonas claras). También cuenta con un buscador para escribir el nombre de la colonia de interés.

<img src="Imágenes/IRCII_demo.png" width="700">

___

### Estadística descriptiva de la vivienda y la dinámica familiar por municipio en Guanajuato.

El siguiente gráfico fue construido mediante el lenguaje de programación [R](https://www.r-project.org), manipulado en el entorno de desarrollo integrado (IDE) [R Studio](https://www.rstudio.com). 

La intención fue la de explorar el panorama de la vivienda y la dinámica familiar de Guanajuato, a través de la relación entre rezago habitacional y hacinamiento, acompañada por la violencia intrafamiliar como variable que podría estar asociada con dicha relación. La matriz de datos fue construida a partir de los indicadores de desarrollo social del estado de Guanajuato que puede descargarse [aquí](http://seieg.iplaneg.net/ind35/). Este gráfico también puede hacerse interactivo en formato .html

Las librerías y el código utilizados para este gráfico interactivo es el siguiente:


```{r}
#Librerías necesarias.

library(readr)
library(plotly)
library(ggplot2)
library(tidyverse)
library(ggExtra)
```

```{r}
#Cargar la matriz de datos.

Matriz_indicadores <- read_delim("Indicadores_GTO/Matriz_indicadores.csv", 
                                 ";", escape_double = FALSE, trim_ws = TRUE)
View(Matriz_indicadores)
```

```{r}
# Graficar un diagrama de dispersión con:
# 3 variables cuantitativas (2 para los ejes, 1 para el tamaño de los puntos)
# 1 variable cualitativa (para el color de los puntos)
# indicando los valores promedio para cada eje con una línea punteada
# modificando las etiquetas de los ejes e incluyendo título
# y asignándola a un objeto.
    
grafica1 <- Matriz_indicadores %>% ggplot(aes(x=rez_hab, y=hacinamiento, size=viol_intr, label=Var_clve)) +
  geom_point(alpha=0.5) +
  scale_size(range = c(.1,15), name="Violencia intrafamiliar") +
  theme_classic() +
  geom_vline(aes(xintercept=mean(rez_hab)), linetype=2, color="lightgrey")  +
  geom_hline(aes(yintercept=mean(hacinamiento, na.rm = T)), linetype=2, color="lightgrey") +
  xlab("Rezago de vivienda por municipio") +
  ylab("Hacinamiento por municipio") +
  ggtitle("Panorama general de la vivienda y la dinámica familiar en Guanajuato")

```

![image](https://user-images.githubusercontent.com/85447979/121120156-a170e980-c7e2-11eb-8cbf-add03ce4e66f.png)

___

### Teledetección y Análisis de Uso de Suelo en León, Guanajuato.

En este proyecto se abordo retrospectivametne la expansión de la ciudad de León, contrastando el crecimiento del entorno construido y el suelo urbano con el crecimiento de la población desde 1980 hasta el 2020, divido en cortes de 20 años. En este mapa interactivo se incluyen los parques industriales dentro del municipio, poniendo en relieve que no hay una correspondacia directa, en términos geográficos, entre las zonas de la ciudad que han mostrado mayor crecimiento, y aquellas en donde se han instalado actividades industriales. De esta forma, se sugiere que el entorno construido de la ciudad crece a más velocidad y con más envergadura que la población misma, aunque esto no se traducen en que existan más oportunidades de vivienda, trabajo y servicios para ésta.

<img src="Imágenes/LULC_Leon.png" width="1200">
___

