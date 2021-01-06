# ELPGV:Ensemble learning for integrative prediction of genetic values with genomic variants. <br>
![](https://halobi.com/wp-content/uploads/2016/08/r_logo.png "R logo")
![](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcS3RzhXKSfXpWhWhvClckwi1Llj1j3HvjKpjvU8CQv4cje23TwS "windows logo")
# Brief introduction <br>
Whole genome variants offer sufficient information for genetic prediction of human disease, 
and animal/plant breeding values that has been widely accepted for animal breeding. 
Many sophisticate statistical algorithms have been developed for enhancing the prediction accuracy;
however, each method has its own advantages and disadvantages, so far no method can beat anther. 
We herein propose a new ensemble learning strategy, called ELPGV (Ensemble Learning of Prediction for
Genetic Value) for genetic prediction, which assembles predictions from several basic methods, 
to more accurate predictions.
## Version and download <br>
* [Version 0.1.0](https://github.com/GuLinLin-JMU/ELPGV/archive/master.zip) -First version released on Jan, 6th, 2021<br>
## Running build-in data
```R
library("ELPGV")
data(exdata)
train_PredMat = mkg$train
test_PredMat = mkg$test[,-1]
TBV = mkg$test[,1]           # True breeding value of testing group
ELPGV_pred = ELPGV(rep_times = 100, interation_times=20, weight_min=0, weight_max=1, 
                   weight_dimension=ncol(test_PredMat), rate_min=-0.01, rate_max=0.01, 
				   paticle_number=20, CR = 1.0, train_PredMat=as.matrix(train_PredMat),
                   test_PredMat=as.matrix(test_PredMat), R = 0.5,IW = 1, AF1 = 2, 
				   AF2 = 2, type ="pcc", select="auto", index=NULL)
PredMat = cbind(TBV,ELPGV_pred)
colnames(PredMat) = c("obs", "BayesA", "BayesB", "BayesCpai", "GBLUP", "ELPGV")
cor(PredMat)
```
## Quick running your data
```R
library("ELPGV")
#loading training predictions
train_PredMat = read.table(system.file("exampleFile/exampleTrainingFile.txt", package = "ELPGV"), header = T)
#loading testing predictions
test_PredMat = read.table(system.file("exampleFile/exampleTestingFile.txt", package = "ELPGV"), header = T)
ELPGV_pred = ELPGV(rep_times = 100, interation_times=20, weight_min=0, weight_max=1, 
                   weight_dimension=ncol(test_PredMat), rate_min=-0.01, rate_max=0.01, 
				   paticle_number=20, CR = 1.0, train_PredMat=as.matrix(train_PredMat),
                   test_PredMat=as.matrix(test_PredMat), R = 0.5,IW = 1, AF1 = 2, 
				   AF2 = 2, type ="pcc", select="auto", index=NULL)
colnames(ELPGV_pred) = c("BayesA", "BayesB", "BayesCpai", "GBLUP", "ELPGV")
head(ELPGV_pred)
```
## How to access help
If users have any bugs or issues or any suggestions are available, feel free to contact:
Linlin Gu: gulinlin_141006@163.com 
Prof. Ming Fang: fangming618@126.com
