# ELPGV
Ensemble learning for integrative prediction of genetic values with genomic variants.
# Brief introduction
Whole genome variants offer sufficient information for genetic prediction of human disease, and animal/plant breeding values that has been widely accepted for animal breeding. Many sophisticate statistical algorithms have been developed for enhancing the prediction accuracy; however, each method has its own advantages and disadvantages, so far no method can beat anther. We herein propose a new ensemble learning strategy, called ELPGV (Ensemble Learning of Prediction for Genetic Value) for genetic prediction, which assembles predictions from several basic methods, to more accurate predictions.
# Running build-in data
library("ELPGV")
data(exdata)
train_PredMat = mkg$train
test_PredMat = mkg$test[,-1]
TBV = mkg$test[,1]           # True breeding value of testing group
ELPGV_pred = ELPGV(rep_times = 100, interation_times=20, weight_min=0, weight_max=1, 
                   weight_dimension=ncol(test_PredMat), rate_min=-0.01, rate_max=0.01, 
                   paticle_number=20, CR=1.0, train_PredMat=as.matrix(train_PredMat),
                    test_PredMat=as.matrix(test_PredMat), R = 0.5,IW = 1, AF1 = 2, 
                    AF2 = 2, type ="pcc", select="auto", index=NULL)
PredMat = cbind(TBV,ELPGV_pred)
colnames(PredMat) = c(“obs”, “BayesA”, “BayesB”, “BayesCpai”, “GBLUP”, “ELPGV”)
cor(PredMat)
