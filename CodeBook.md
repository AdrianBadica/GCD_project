GCD_project
===========
# Data Source

The data contained in this project is available from : 
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

The database was built from the recordings of 30 subjects performing activities of daily living (ADL) 
while carrying a waist-mounted smartphone with embedded inertial sensors.

##For each record it was provided:
======================================

* Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
* Triaxial Angular velocity from the gyroscope. 
* A 561-feature vector with time and frequency domain variables. 
* Its activity label. 
* An identifier of the subject who carried out the experiment.


##The dataset includes the following files:
=========================================

* 'README.txt'
* 'features_info.txt': Shows information about the variables used on the feature vector.
* 'features.txt': List of all features.
* 'activity_labels.txt': Links the class labels with their activity name.
* 'train/X_train.txt': Training set.
* 'train/y_train.txt': Training labels.
* 'test/X_test.txt': Test set.
* 'test/y_test.txt': Test labels.

##The following files are available for the train and test data. Their descriptions are equivalent. 

* 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. 
Its range is from 1 to 30. 
* 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer
X axis in standard gravity units 'g'. Every row shows a 128 element vector. The same description applies 
for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 
* 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting 
the gravity from the total acceleration. 
* 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope 
for each window sample. The units are radians/second. 

##Citation Request:

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition 
on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of
Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012





# Transformations made to the original dataset

## In order to give the dataset a more appropiate form and to enhance readibility, several transformations
have been made, using R, described below (see the Readme.md file for the code used) :
* the X_train and X_test files have been aggregated to include all the observations
* the names from the features.txt file have been added to the dataset (each column representing a measurement)
* the Y_train and Y_test files have been merged, containing the activities for which the measurements have been made
* the activity_labels.txt was loaded into R and linked to the activities from the step above in order to have 
their descriptive names
* the files with the subjects that have been observed (subject_train.txt and subject_test.txt) were loaded and merged
* then the variables, the activities and the subjects were merged to create the complete original dataset


## Summarizing and creating the tidy dataset :
* from the complete dataset only the measurements for the means and standard deviations have been selected :
*'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions
* Time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz
* The body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ)
* Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag).

tBodyAcc-XYZ 
tGravityAcc-XYZ 
tBodyAccJerk-XYZ 
tBodyGyro-XYZ
tBodyGyroJerk-XYZ 
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

* the names of the variables have been further cleaned by eliminating hyphens and parenthesis
* for each subject and for each activity the average for each of the selected measurements has been calculated
* the resulting dataset can be written as a .txt file



