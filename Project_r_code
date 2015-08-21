#Getting and cleaning data project

# Download the file if necessary
library(data.table)
fileURL = 'https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip '
zipName = "Dataset.zip"
if (!file.exists(zipName)) {
  download.file(fileURL, destfile = zipName)
}

# Read the required files

activity_labels <- read.table(unz(zipName, "UCI HAR Dataset/activity_labels.txt"), header=F, quote="\"", sep=",", stringsAsFactors=FALSE, fill = T)
features <- read.table(unz(zipName, "UCI HAR Dataset/features.txt"), header=F, quote="\"", sep="|", stringsAsFactors=FALSE, fill = T)

test_x_test = read.table(unz(zipName, "UCI HAR Dataset/test/X_test.txt"), header=F, quote="\"", sep=" ", colClasses=c(rep("numeric", 561), rep("NULL", 110)),fill = T)
test_y_test = read.table(unz(zipName, "UCI HAR Dataset/test/y_test.txt"), header=F, quote="\"", sep=" ",  stringsAsFactors=FALSE,fill = T)
test_subject = read.table(unz(zipName, "UCI HAR Dataset/test/subject_test.txt"), header=F, quote="\"", sep=" ",  stringsAsFactors=FALSE,fill = T)

train_x_test = read.table(unz(zipName, "UCI HAR Dataset/train/X_train.txt"), header=F, quote="\"", sep=" ", colClasses=c(rep("numeric", 561), rep("NULL", 110)), fill = T)
train_y_test = read.table(unz(zipName, "UCI HAR Dataset/train/y_train.txt"), header=F, quote="\"", sep=" ",  stringsAsFactors=FALSE,fill = T)
train_subject = read.table(unz(zipName, "UCI HAR Dataset/train/subject_train.txt"), header=F, quote="\"", sep=" ",  stringsAsFactors=FALSE,fill = T)


# add column names
colnames(activity_labels) = c("activity_label")
colnames(test_subject) = c("subject")
colnames(train_subject) = c("subject")

colnames(test_y_test) = c("activity")
colnames(train_y_test) = c("activity"))

vfeatures = features[,1]
setnames(test_x_test, vfeatures)
setnames(train_x_test, vfeatures)

# combine the data
test_data = cbind(test_subject, test_y_test, test_x_test[1:2947,])
train_data = cbind(train_subject, train_y_test, train_x_test[1:7352,])
all_data = rbind(test_data, train_data)

#determine the list of that we want to extract from the table
subset_features = vfeatures[grepl(".*std[(].*", vfeatures) | grepl(".*mean[(].*", vfeatures)]
sel_columns = c("activity", "subject")
sel_columns = append(sel_columns, subset_features)

# select only the desired columns
filtered_data = all_data[sel_columns]

# Look up the activity labels to go with the activities
library(sqldf)

final_data = sqldf("select activity_label, a.* from filtered_data a, activity_labels l where a.activity = substr(l.activity_label,1,1)")

# aggregate based on activity and subject
agg = aggregate(final_data, list(final_data$subject, final_data$activity_label), mean, na.rm = TRUE)

write.table(agg, file="tidy_dataset.txt", row.name = FALSE)
