
#Reading training tables - xtrain / ytrain, subject train
xtrain = read.table("./UCI HAR Dataset/train/X_train.txt")
ytrain = read.table("./UCI HAR Dataset/train/Y_train.txt")
subject_train = read.table("./UCI HAR Dataset/train/subject_train.txt")

#Reading the testing tables
xtest = read.table("./UCI HAR Dataset/test/X_test.txt")
ytest = read.table("./UCI HAR Dataset/test/Y_test.txt")
subject_test = read.table("./UCI HAR Dataset/test/subject_test.txt")

#Read the features data
features = read.table("./UCI HAR Dataset/features.txt")

#Read activity labels data
activityLabels = read.table("./UCI HAR Dataset/activity_labels.txt")

#Create Sanity and Column Values to the Train Data
colnames(xtrain) = features[,2]
colnames(ytrain) = "activityId"
colnames(subject_train) = "subjectId"
#Create Sanity and column values to the test data
colnames(xtest) = features[,2]
colnames(ytest) = "activityId"
colnames(subject_test) = "subjectId"
#Create sanity check for the activity labels value
colnames(activityLabels) <- c('activityId','activityType')

#1 Merging the train and test data - important outcome of the project
mrg_train = cbind(ytrain, subject_train, xtrain)
mrg_test = cbind(ytest, subject_test, xtest)
#Create the main data table merging both table tables - this is the outcome of 1
setAllInOne = rbind(mrg_train, mrg_test)

#2. Extracts only the measurements on the mean and standard deviation for each measurement.
# Need step is to read all the values that are available
colNames = colnames(setAllInOne)
#Need to get a subset of all the mean and standards and the correspondongin activityID and subjectID 
mean_and_std = (grepl("activityId" , colNames) | grepl("subjectId" , colNames) | grepl("mean.." , colNames) | grepl("std.." , colNames))
#A subtset has to be created to get the required dataset
setForMeanAndStd <- setAllInOne[ , mean_and_std == TRUE]

# 3. Uses descriptive activity names to name the activities in the data set
setWithActivityNames = merge(setForMeanAndStd, activityLabels, by='activityId', all.x=TRUE)

# 4. Appropriately labels the data set with descriptive variable names.
# New tidy set has to be created 
secTidySet <- aggregate(. ~subjectId + activityId, setWithActivityNames, mean)
secTidySet <- secTidySet[order(secTidySet$subjectId, secTidySet$activityId),]

# 5. From the data set in step 4, creates a second, independent tidy data set with the average
# of each variable for each activity and each subject.

#The last step is to write the ouput to a text file 
write.table(secTidySet, "secTidySet.txt", row.name=FALSE)
