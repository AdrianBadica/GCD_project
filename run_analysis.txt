## see where your working directory is if you need to put the data files into it

#getwd()

## or you can set your working directory where the files are
#setwd(dir)


## read the X_train and X_test files into R and merge them
x_train <- read.table("X_train.txt")
x_test <- read.table("X_test.txt")
x  <- rbind(x_train,x_test)

## read the variables names into R
features <- read.table("features.txt")

## set the column names based on the features.txt and create a new data table named "data"

data <- x
names(data) <- features[,2]

## read the y_train and y_test into R (these are the activities performed) and merge them
y_train <- read.table("y_train.txt")
y_test <- read.table("y_test.txt")
y <- rbind(y_train,y_test)

## set a more descriptive name
names(y) <- "activityID"

## read the activity labels
a_labels <- read.table("activity_labels.txt")

## load the sqldf package to set appropiate names for the activities
library(sqldf)
act <- sqldf("select y.activityID, a_labels.V2 as actDesc from y join a_labels where y.activityID = a_labels.V1 ")

## read the files with the subjects that have performed the activities
subject_train <- read.table("subject_train.txt")
subject_test <- read.table("subject_test.txt")
subject <- rbind(subject_train,subject_test)

## set a more descriptive name
names(subject) <- "subjectID"

## put them all together to create the complete dataset ( subject, activity, measurements from train and test sets with column names)

dataset <- cbind(subject,act,data)
# View(dataset)

##################################################################################################################
##################################################################################################################


## select only the columns with measurements for standard deviation (std)
std_m <- dataset[,grep("std", names(dataset))]


## select only the columns with measurements for means (mean)
mean_m <- dataset[,grep("mean", names(dataset))]

## merge them to create the working dataset, including subjects and activities

wdataset  <- cbind(subject, act, mean_m,std_m)
#View(wdataset)

## drop the activityID column
wdataset[,2]=NULL
#View(wdataset)

##clean the names of the variables (take the "-" and the "()" out)
v <- names(wdataset)
v2 <- gsub("-","",v)
v3 <- gsub("\\(\\)","",v2)
names(wdataset) <- v3
#View(wdataset)

########## creating the tidy dataset ##########

library(reshape2)
plm <- melt(wdataset, id.vars=c("subjectID","actDesc"))
stf <- dcast(plm, subjectID + actDesc ~ variable, mean)
tidydata <- stf

## exporting to a tab delimited txt file, named "mytidydata", on the C:/ directory
write.table(tidydata, "c:/mytidydata.txt", sep="\t") 
