# Quiz-1_parte-2

# Quiz 1: Introducción a R. Funciones y ciclos
# Instrucciones: https://drive.google.com/file/d/1GhAQcVyQCJu0RxvkQXSymsw3lNzgi_BD/view?usp=sharing
# Datos: https://docs.google.com/spreadsheets/d/1GuceAEA80SvL-mGap0T0nUjIx2dr0X4G/edit#gid=645815873 

library(readxl) 
library(xts)    

setwd("C:/Users/HP/Documents/Proyecto/Programacion") 

#Cargando datos: 
Data <- read_excel("ejemplo promedios moviles centrados.xlsx", sheet="Smooth", range = "A2:B632")
D$Fecha <- as.Date(D$f)

#Dando estructura de series de tiempo:
ffr <- xts(D$'ffr', order.by = seq(as.Date('1954-07-31'), length.out = NROW(D), by="month"))
ffr <- ts(D$'ffr', start=c(1954,7), frequency=12) 
