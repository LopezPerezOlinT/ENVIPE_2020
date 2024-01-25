#Primero vamos a necesitar los datos que puedes encontrar y descargar en
#los siguientes enlaces.

#Dirección Base de datos ENVIPE 2020 
#https://drive.google.com/file/d/1ve6gQzckeGmKFbU6vTDoC_NT7OkoKiYg/view

#Dirección descriptor_2020
#https://drive.google.com/file/d/1UJYMz4HZhHtah7gtRkhUG0f8aKCigdAA/view

#aquí voy a cargar la base de datos, recuerda que cambia con respecto en 
#donde lo guarda cada quien dentro de su computadora, usa un scrip normal de Rstudio
#para que no se tarde en generar el pdf/word/html generamos los objetos de la base de datos
#que necesitaremos en un scrip dentro de Rstudio

library(foreign)
library(tidyverse)

setwd("C:\\Users\\López Pérez Olin Ton\\Documents\\Archivos de R\\Scidata R\\EMVIPE_2020")

tper_vic <- read.dbf("TPer_Vic1.dbf")
tmod_vic <- read.dbf("TMod_Vic.dbf")
tvivienda <- read.dbf("TVivienda.dbf")

descriptor_del <- read_tsv("descriptor_2020.csv")

catalogo_entidades <- data.frame("CVE_ENT"=unique(tvivienda$CVE_ENT),
                                 "NOM_ENT"=unique(tvivienda$NOM_ENT))

tmod_vic <- left_join(tmod_vic,descriptor_del,by=c("BPCOD"="CODIGO"))

save(list = c("tper_vic",
              "tmod_vic",
              "descriptor_del",
              "catalogo_entidades"),
     file = "envipe_2020.RData")

#En el renglon 21 del código dice num_entidad = 1 ; aqui cambiando el número
#hace el analizis de cada identidad federativa (del 1 hasta el 32)

#ten en cuenta que esta es ENVIPE_2020; es decir la encueta que se realizo para méxico en 2019
#si deseas hacer otro analisis de envipes más recientes o más antiguas ve a 
#https://www.inegi.org.mx/programas/envipe/2023/
