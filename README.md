# EVALUACION3
getwd()
setwd("curso_R_basico")

data1<-read.table("./educacion_04.csv", sep = ",",header=TRUE) 
data2<-read.table("./educacion_03.csv", sep = ",", header = TRUE)
data3 <-read.table("./educacion_01.csv", sep = ",",header = TRUE)

##Para obtener las columnas de interes de cada base de datos 

tabla1<- data1[,-1]
tabla1<-tabla1[,-2]
tabla1<-tabla1[,-6]
tabla1<-tabla1[,-7]
tabla1<-tabla1[,-9]
tabla2<-data2[,-1]
tabla2<-tabla2[,-2]
tabla2<-tabla2[,-4]
tabla3<-data3
tabla3<-data3[,-1]
tabla3<-tabla3[,-2]
tabla3<-tabla3[,-4]


##Para ver qué nombres en común tiene mi base de datos 

intersect(names(tabla1), names(tabla2))
intersect(names(tabla1), names(tabla3))
educacion_tabla<-merge(tabla1,tabla2, all = TRUE)
educacion_tabla <-merge(educacion_tabla,tabla3)

##Para agrupar la información de cada variable de mi base de datos 

install.packages("tidyr")
library(tidyr)
educacion <- educacion_tabla[,c("Sin.escolaridad", "Preescolar", "Primaria", "Secundaria", "Preparatoria.o.bachillerato","Licenciatura.o.equivalente","Posgrado","Asiste","No.asiste","Sabe.leer.y.escribir","No.sabe.leer.y.escribir")]
educacion <- gather(educacion, escolaridad, valor, Sin.escolaridad:Posgrado)
educacion <-gather(educacion,condición.de.asistencia.escolar,valor,Asiste:No.asiste)
educacion <-gather(educacion,aptitud.de.leer.y.escribir,valor,Sabe.leer.y.escribir:No.sabe.leer.y.escribir)

##Para exportar la base de datos 

write.csv(condicion.educacion,"./condicion.educacion.csv")
```
