---
title: "Segunda Tarea"
author: "Allan Marín Campos"
---

## Graficación sobre la calidad del café según el Instituto de calidad del café (CQI)

### Grupo 002

#### Introducción

Este docummento presenta datos relacionados con la calidad del café, en el cual se utiliza el lenguaje de programación R, visto en clase, el cual crea tablas y graficos de gran ayuda para el entendimiento del tema a desarrollar. 

Para este trabajo, utilizaremos un conjunto de datos suministrados por el [Coffee Quality Institute (CQI)](https://github.com/fatih-boyar/coffee-quality-data-CQI), los cuales fueron tomados desde el siguiente enlace https://github.com/fatih-boyar/coffee-quality-data-CQI. Este repositorio incluye muestras de café de diferentes partes del mundo. Estos datos contienen información detallada sobre el país de origen, la altitud, la variedad, el color y el método de procesamiento del café, así como las evaluaciones de diversas características, como aroma, sabor, acidez y puntaje total.

Nuestra meta para este proyecto es utilizar los conocimientos adquiridos en clase y los datos necesarios para realizar graficos y tablas los cuales muestren el analisis de los datos que nos ayuden a comprender mejor los factores que influyen en la calidad del café.

## Carga de paquetes de R

```{r}
#| label: Carga-datos
#| warning: false
library(DT)
library(ggplot2)
library(plotly)
library(dplyr)
library(tidyverse)
library(ggthemes)
library(readr)
```

## Tabla DT

```{r}
# Tabla de datos
# Leer el archivo coffee-quality.csv 
coffee_data <- read.csv(
  "C:/Users/marin/Downloads/TAREA2_Procesamiento/coffee-quality.csv"
)

# Crear la tabla interactiva con el paquete DT
datatable(coffee_data[, c("Country_of_Origin", "Variety", "Color", "Altitude", "Total_Cup_Points")],
          options = list(pageLength = 10, lengthMenu = c(10, 20, 50)),
         filter="top")
```

# Histograma

```{r}

# Histograma que muestre la distribución de la variable Total_Cup_Points

p <- ggplot(coffee_data, aes(x = Total_Cup_Points)) +
  geom_histogram(binwidth = 1, color = "white", fill = "blue") +
  geom_density(alpha = 0.2, fill = "red") +
  labs(title = "Distribución de Total Cup Points",
       x = "Total Cup Points",
       y = "Frecuencia") +
  theme_test()

# Convertir el gráfico a plotly para hacerlo interactivo
ggplotly(p)

```

# Gráfico de dispersión

```{r}
# Gráfico de dispersión de Altitude (altitud, en el eje x) vs Total_Cup_Points (puntaje total, en el eje y)
p <- ggplot(coffee_data, aes(x = Altitude, y = Total_Cup_Points)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE, color = "green") +
  labs(title = "Relación entre Altitude y Total Cup Points",
       x = "Altitude",
       y = "Total Cup Points") +
  theme_test()

# Convertir el gráfico a plotly para hacerlo interactivo
ggplotly(p, tooltip = c("Altitude", "Total_Cup_Points"))

```

# Gráfico de caja

```{r}
# Gráfico de caja que muestre las estadísticas (cuartiles, mínimos, máximos y valores atípicos) de la variable Total_Cup_Points (puntaje total) para cada valor de la variable Color (color)

p <- ggplot(coffee_data, aes(x = Color, y = Total_Cup_Points)) +
  geom_boxplot() +
  labs(title = "Distribución de Total Cup Points por Color",
       x = "Color",
       y = "Total Cup Points") +
  theme_test() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Convertir el gráfico a plotly para hacerlo interactivo
ggplotly(p)

```
