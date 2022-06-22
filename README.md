# Quiz-1_parte-2

# Quiz 1: Introducción a R. Funciones y ciclos
# Instrucciones: https://drive.google.com/file/d/1GhAQcVyQCJu0RxvkQXSymsw3lNzgi_BD/view?usp=sharing
# Datos: https://docs.google.com/spreadsheets/d/1GuceAEA80SvL-mGap0T0nUjIx2dr0X4G/edit#gid=645815873 

rm(list = ls())
library(readxl) 
library(xts)    

setwd("C:/Users/HP/Documents/Proyecto/Programacion") 

#Cargando datos: 
Data <- read_excel("ejemplo promedios moviles centrados.xlsx", sheet="Smooth", range = "A1:B632")
Data$fecha <- as.Date(Data$f)

#Dando estructura de series de tiempo:
ffr <- xts(Data$`ffr`, order.by = seq(as.Date('1954-07-31'), length.out = NROW(Data), by="month"))
ffr <- ts(Data$`ffr`, start=c(1954,7), frequency=12) 

#Estableciendo funcion:
PM <- function(X, K) {
  obs <- length(X)
  pm <- c()
  if (K %% 2 == 0) {
    E <-  K/2
    for (i in (E+1):(obs-E)){
      x <- (1/(2*K))*(sum(ffr[(i-E):(i+E-1)]) + sum(ffr[(i-E+1):(i+E)]))
      pm <- rbind(pm, x)
    }
    miss <- data.matrix(rep(NA, E))
    pm <- rbind(miss, pm, miss)
    
  } else {
    E <- (K-1)/2
    for (t in (E+1):(obs-E)){
      x <- (1/K)*(sum(ffr[(t-E):(t+E)]))
      pm <- rbind(pm, x)
    }
    miss <- data.matrix(rep(NA, E))
    pm <- rbind(miss, pm, miss)
  }
  return(pm)
}
