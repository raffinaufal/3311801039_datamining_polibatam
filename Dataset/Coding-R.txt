#lokasi-file
lokasi_kerja <- "E:/suicide"
setwd(lokasi_kerja)
getwd()

#install-packages
install.packages("cluster")
install.packages("fpc")
install.packages("ggplot2")
install.packages("rJava")

#set-library
library("cluster")
library("fpc")
library("ggplot2")
library("rJava")

#Import-data
starbucks <- read.csv("starbucks.csv", sep = ",")
#Duplikatdata-HilangkanKolomMenu
starbucks.f = starbucks
starbucks.f$Menu <- NULL
View (starbucks.f)

#Normalisasi
starbucks.stand <- scale(starbucks.f[-1])

#view
View(starbucks.stand)
head(starbucks.stand)
starbucks.stand$Menu

#Membuat-Cluster-dengan-K-Means
set.seed (8953)
hasil <- kmeans(starbucks.stand, 3)
hasil

#View-Satu2
hasil$cluster
#Untuk Melihat Jumlah anggota di tiap cluster
hasil$size
hasil$centers

#Tampilkan-Menu
table(starbucks$Menu, hasil$cluster)

#plot1
plot(starbucks.stand, col = hasil$cluster)
#points
points(hasil$centers, col = 2:6, pch = 8, cex = 2)
#Plot2
clusplot(starbucks.stand, hasil$cluster, color = T, shade = T, table = 2, lines = 0)

