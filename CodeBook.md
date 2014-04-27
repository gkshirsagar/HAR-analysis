HAR-analysis
============
Clean-up and collate data contained in several tables recording detailed parameters on human activity in the Human Activity Recognition experiments using smartphones.

## Description
This CodeBook documents how collected data was filtered, merged and reshaped to output the final summarized information.

## Original Data
Original dataset was downloaded from the url https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip. Here's a link to the project for a full description: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones.
It was obtained in an archive `getdata-projectfiles-UCI HAR Dataset.zip`. On unzipping, it produced a directory `UCI HAR Dataset` which contained the data files.
The data was spread across multiple files in multiple directories. Only a part of the data files provided were used for analysis and data files that weren't required were left untouched.

## Data Files
The data files that were used for analysis are:
* `UCI HAR Dataset/activity_labels.txt`: Descriptive names for human activities recognized by the devices.
* `UCI HAR Dataset/features.txt`: Names of features whose measurements were recorded by the sensors.
* `UCI HAR Dataset/train`: Directory containing training data for the devices. This comprises 70% of the total data.
* `UCI HAR Dataset/train/X_train.txt`: Data file containing measurements recorded for 561 different parameters.
* `UCI HAR Dataset/train/y_train.txt`: Data file containing activities recognized for each row of measurements.
* `UCI HAR Dataset/train/subject_train.txt`: Data file containing the subject whose device made the measurements.
* `UCI HAR Dataset/test`: Directory containing test data for the devices. This comprises 30% of the total data.
* `UCI HAR Dataset/test/X_test.txt`: Data file containing measurements recorded for 561 different parameters.
* `UCI HAR Dataset/test/y_test.txt`: Data file containing activities recognized for each row of measurements.
* `UCI HAR Dataset/test/subject_test.txt`: Data file containing the subject whose device made the measurements.

## Step-by-step Analysis
1. Corresponding data files from the training set and test are merged to create unified data. Training data had 7352 records and test data had 2947 records, for a total of 10299 records.
2. `UCI HAR Dataset/train/subject_train.txt` was merged with `UCI HAR Dataset/test/subject_test.txt` and read into a table called `subjectTable` in R.
3. `UCI HAR Dataset/train/y_train.txt` was merged with `UCI HAR Dataset/test/y_test.txt` and read into a table called `activityTableRaw` in R.
4. The descriptive names for activities were read from `UCI HAR Dataset/activity_labels.txt` and a new table `activityTable` was created with the activity names for activity codes in R.
5. For the purpose of this analysis, we required only those sensor measurements which were 'mean' or 'standard deviation'. There were 33 each of such columns, amounting to 66 columns of measurements.
6. `UCI HAR Dataset/features.txt` was read to obtain feature names.
7. A required columns vector was created in R to read only those columns from the data files containing the required features.
8. `UCI HAR Dataset/train/X_train.txt` was merged with `UCI HAR Dataset/test/X_test.txt` and read into a table called `readingsTable` in R with only the required 66 columns.
9. The 3 tables `subjectTable`, `activityTable`, `readingsTable` were given appropriate column names.
10. The 3 tables were then merged together to obtain the master table containing data for all subjects for all activities for the required measurements, named as `mergedTable` in R. This table had 10299 rows and 68 columns.
11. To obtain a short, summarized, tidy representation of the master table, it was grouped by subject first and then activities and then collapsed to summarize just the means for each measurement. This table had 180 rows (30 subjects x 6 activities) and 68 columns.
12. A tidy data set was exported as a text file and provided for viewing.

## Names of Columns in the Tidy Table
* Subject: subject code; type: `factor`; value: `1:30`.
* Activity: activity label; type: `factor`; value: `WALKING`, `WALKING_UPSTAIRS`, `WALKING_DOWNSTAIRS`, `SITTING`, `STANDING`, `LAYING`
For the following columns: type: `numeric`; value: `[-1.0, 1.0]`.
* tBodyAcc-mean()-X
* tBodyAcc-mean()-Y
* tBodyAcc-mean()-Z
* tBodyAcc-std()-X
* tBodyAcc-std()-Y
* tBodyAcc-std()-Z
* tGravityAcc-mean()-X
* tGravityAcc-mean()-Y
* tGravityAcc-mean()-Z
* tGravityAcc-std()-X
* tGravityAcc-std()-Y
* tGravityAcc-std()-Z
* tBodyAccJerk-mean()-X
* tBodyAccJerk-mean()-Y
* tBodyAccJerk-mean()-Z
* tBodyAccJerk-std()-X
* tBodyAccJerk-std()-Y
* tBodyAccJerk-std()-Z
* tBodyGyro-mean()-X
* tBodyGyro-mean()-Y
* tBodyGyro-mean()-Z
* tBodyGyro-std()-X
* tBodyGyro-std()-Y
* tBodyGyro-std()-Z
* tBodyGyroJerk-mean()-X
* tBodyGyroJerk-mean()-Y
* tBodyGyroJerk-mean()-Z
* tBodyGyroJerk-std()-X
* tBodyGyroJerk-std()-Y
* tBodyGyroJerk-std()-Z
* tBodyAccMag-mean()
* tBodyAccMag-std()
* tGravityAccMag-mean()
* tGravityAccMag-std()
* tBodyAccJerkMag-mean()
* tBodyAccJerkMag-std()
* tBodyGyroMag-mean()
* tBodyGyroMag-std()
* tBodyGyroJerkMag-mean()
* tBodyGyroJerkMag-std()
* fBodyAcc-mean()-X
* fBodyAcc-mean()-Y
* fBodyAcc-mean()-Z
* fBodyAcc-std()-X
* fBodyAcc-std()-Y
* fBodyAcc-std()-Z
* fBodyAccJerk-mean()-X
* fBodyAccJerk-mean()-Y
* fBodyAccJerk-mean()-Z
* fBodyAccJerk-std()-X
* fBodyAccJerk-std()-Y
* fBodyAccJerk-std()-Z
* fBodyGyro-mean()-X
* fBodyGyro-mean()-Y
* fBodyGyro-mean()-Z
* fBodyGyro-std()-X
* fBodyGyro-std()-Y
* fBodyGyro-std()-Z
* fBodyAccMag-mean()
* fBodyAccMag-std()
* fBodyBodyAccJerkMag-mean()
* fBodyBodyAccJerkMag-std()
* fBodyBodyGyroMag-mean()
* fBodyBodyGyroMag-std()
* fBodyBodyGyroJerkMag-mean()
* fBodyBodyGyroJerkMag-std()

Details on the measurement values:
These are measurements recorded from sensors and were used to recognize the activities of the humans.
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.
More details on these signals can be found in the documentation with the data set in `UCI HAR Dataset/features_info.txt`.
