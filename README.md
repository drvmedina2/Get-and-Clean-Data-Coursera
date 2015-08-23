# Get-and-Clean-Data-Coursera

####Because i wasn´t able to push the script to GitHub, i copied and pasted it on plain text, to show my worke done. The terminal on Mac just refused to push the script. Here is my work:
setwd("~/UCI HAR Dataset 2")


library(plyr); library(dplyr)


caract <- read.table("./features.txt");
et_activ <- read.table("./activity_labels.txt")

pru_suj <- read.table("./test/subject_test.txt")
pruebaX <- read.table("./test/X_test.txt")
pruebaY <- read.table("./test/Y_test.txt")
colnames(et_activ) <- c("ident_act", "tipo_act" )
colnames(pru_suj) <- "ident_suj"
colnames(pruebaX) <- caract [,2]
colnames(pruebaY) <- "ident_act"
entr_suj <- read.table("./train/subject_train.txt")
entrX <- read.table("./train/X_train.txt")
entrY <- read.table("./train/Y_train.txt")
colnames(entr_suj) <- "ident_suj"
colnames(entrX) <- caract[ ,2]
colnames(entrY) <- "ident_act"

##Merge data sets with x and y values based on tests and train parameters
prueba_entr1 <- rbind(pruebaX, entrX)
prueba_entr2 <- rbind(pruebaY, entrY)
prueba_entrSuj <- rbind(entr_suj, pru_suj)


Assign descriptive names to activities on data set, correct them and
label the data set with descriptive variables
prueba_entr2[, 1] <- et_activ[prueba_entr2[, 1], 2]
names(prueba_entr2) <- "activity"
names(prueba_entrSuj) <- "subject"
##label the data set with descriptive variables
prueba_entr2[, 1] <- et_activ[prueba_entr2[, 1], 2]
names(prueba_entr2) <- "activity"
names(prueba_entrSuj) <- "subject"

Create the final and complete data set
resumen <- cbind(prueba_entr1, prueba_entr2, prueba_entrSuj)

Using dplyr, get rid of duplicated columns and extract only the mean and std columns
mean_std_coldupl <- resumen[ !duplicated(names(resumen)) ]
resumen_mean_std <- select(mean_std_coldupl, matches("mean|std|activity|subject"))

Using plyr, and write.table, create a .txt file with the tidy data set
promedios <- ddply(resumen_mean_std, .(subject, activity), function(x) colMeans(x[, 1:66]))

write.table(promedios, "./promedios.txt", row.names = FALSE)





##run_analysis.R, script
This project is intended to demonstrate some skills on obtaining and cleaning data from raw data sets, as part of the Coursera Getting and cleaning data Course.

##Raw data.
The original data sets can be found on this URL: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip, at the UCI Machine Learning Repository. You´ll find some sets of .txt files which contains data about subjects performance and physiological variables obtained from those subjects through wearable gadgets connected to smartphones.

##Running run_analysis.R script
After downloading and unzip the data set, you should store the UCI .txt files on your working directory and overwrite the script to locate the files. Then you´ll be able to set the script setwd()command to your own working directory and run the script over the stored files.

#Instructions
The run_analysis.R script, will obtain a tidy data set from the UCI repository, this data set will reflect the average values over each and every variable, crossed with the user and the activity type recorded by the wearable gadgets and passed to the smartphones.

The tidy data set can be viewed after running thehe script.

##The script
Running the run_analysis.R script: 1.- Set working directory. In this part, setwd() will allow you to reach for the files unzipped and loaded to your working directory 2.-Load dplyr() and plyr(), packages that will be used to get rid of duplicated columns on data sets and allows to select desired columns on lines 41 and 42. 3.- Lines 8 and 9 read the text files containing labels for the final data set 4.- Lines 11 to 23 read the text files containing the values for each train and test values, and the subject and activities lists 5.- Lines 26 to 28 merges and combines the data sets uploaded to R into a single and coherent data frame 6.- Lines 33 to 35 Assign descriptive names to activities on data set, correct them and labels the data set with descriptive variables 7.- Line 38 creates the final complete tidy data set to work with 8.- Line 41 gets rid of duplicated columns to avoid them to interfere while extracting certain variables 9.- Line 42 uses select() function from dplyr() package to select and extract only the variables containing mean and std values from the tidy data set 10.- Finally, Using plyr, and write.table, create a .txt file with the tidy data set

##Warnings
This run_analysis.R script doesn´t follows the exact sequencial steps from the Course Project but complies with each and every steps required, in different order, to finally obtain the requested final tidy data set.

#Code Book
This code book summarizes the resulting data fields in promedios.txt.

##Identifiers

subject 
activity 

##Labels (Activity)

WALKING (value 1): subject was walking during the test
WALKING_UPSTAIRS (value 2): subject was walking up a staircase during the test
WALKING_DOWNSTAIRS (value 3): subject was walking down a staircase during the test
SITTING (value 4): subject was sitting during the test
STANDING (value 5): subject was standing during the test
LAYING (value 6): subject was laying down during the test

##Measurements

tBodyAccMeanX
tBodyAccMeanY
tBodyAccMeanZ
tBodyAccStdX
tBodyAccStdY
tBodyAccStdZ
tGravityAccMeanX
tGravityAccMeanY
tGravityAccMeanZ
tGravityAccStdX
tGravityAccStdY
tGravityAccStdZ
tBodyAccJerkMeanX
tBodyAccJerkMeanY
tBodyAccJerkMeanZ
tBodyAccJerkStdX
tBodyAccJerkStdY
tBodyAccJerkStdZ
tBodyGyroMeanX
tBodyGyroMeanY
tBodyGyroMeanZ
tBodyGyroStdX
tBodyGyroStdY
tBodyGyroStdZ
tBodyGyroJerkMeanX
tBodyGyroJerkMeanY
tBodyGyroJerkMeanZ
tBodyGyroJerkStdX
tBodyGyroJerkStdY
tBodyGyroJerkStdZ
tBodyAccMagMean
tBodyAccMagStd
tGravityAccMagMean
tGravityAccMagStd
tBodyAccJerkMagMean
tBodyAccJerkMagStd
tBodyGyroMagMean
tBodyGyroMagStd
tBodyGyroJerkMagMean
tBodyGyroJerkMagStd
fBodyAccMeanX
fBodyAccMeanY
fBodyAccMeanZ
fBodyAccStdX
fBodyAccStdY
fBodyAccStdZ
fBodyAccMeanFreqX
fBodyAccMeanFreqY
fBodyAccMeanFreqZ
fBodyAccJerkMeanX
fBodyAccJerkMeanY
fBodyAccJerkMeanZ
fBodyAccJerkStdX
fBodyAccJerkStdY
fBodyAccJerkStdZ
fBodyAccJerkMeanFreqX
fBodyAccJerkMeanFreqY
fBodyAccJerkMeanFreqZ
fBodyGyroMeanX
fBodyGyroMeanY
fBodyGyroMeanZ
fBodyGyroStdX
fBodyGyroStdY
fBodyGyroStdZ
fBodyGyroMeanFreqX
fBodyGyroMeanFreqY
fBodyGyroMeanFreqZ
fBodyAccMagMean
fBodyAccMagStd
fBodyAccMagMeanFreq
fBodyBodyAccJerkMagMean
fBodyBodyAccJerkMagStd
fBodyBodyAccJerkMagMeanFreq
fBodyBodyGyroMagMean
fBodyBodyGyroMagStd
fBodyBodyGyroMagMeanFreq
fBodyBodyGyroJerkMagMean
