# Getting Data Project

## Code description

This code will read the accelerometer raw data and combine it to produce a tidy dataset.  The code consists of the following steps:
1. check to see if the data file exists and download it if necessary.

2. Read the following files: _activity labels_ - will be used to map the activity numbers to meaningful names; _features_ - contain the descriptions of the various metrics captured in the data files; _test and train data file_ - each file contains a data file with vectors of sampled metrics and a file with the activity numbers; _subject files_ - contains a single column with the subject number for each obervation

3. give meaningful column names to the raw data - for small sets, like the subject data, we just assign hardcoded values.  For features, we use the vector of feature names read from features.txt

4. now we combine the data:  We first use _cbind_ to paste together the columns, from the activity numbers, subjects and gathered metrics, giving us one data set each for test and train.  Then we use _rbind_ to combine the test and train data sets.

5. next we want to extract only the metrics releaded to means and standard deviations.  We do this by filtering the list of field names for ones that contain either "std(" or "mean(", then extract only those columns from the main dataset.

6. next the code will use SQLDF to execute a join to the activity labels data to look up meaningful labels for the activities

7. finally, we product the tidy dataset by aggregating the data.  This data is tidy because it meets the following criteria:
 - each variable is in one column
 - each observation based on the aggregating fields is on one row
 - we only have one "kind" of data and it is all in one table
 
8. last we write the data to a file.

## Code Book
