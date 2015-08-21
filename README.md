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
This dataset contain average values for the metrics releaded to means and standard deviations by subject and activity.  Following are a list of columns:

activity_label - description of activity                                                                                               
 -  1 WALKING                                                                                                                           
 -  2 WALKING_UPSTAIRS                                                                                                                  
 -  3 WALKING_DOWNSTAIRS                                                                                                                
 - 4 SITTING                                                                                                                           
 -  5 STANDING                                                                                                                          
 - 6 LAYING                                                                                                                            
subject - a number 1-30 identifying a participant in the study                                                                         
001 tBodyAcc-mean()-X         - the average value of the sampled tBodyAcc-mean()-X value for the given subject and activity            
002 tBodyAcc-mean()-Y         - the average value of the sampled tBodyAcc-mean()-Y value for the given subject and activity            
003 tBodyAcc-mean()-Z         - the average value of the sampled tBodyAcc-mean()-Z value for the given subject and activity            
004 tBodyAcc-std()-X          - the average value of the sampled tBodyAcc-std()-X value for the given subject and activity             
005 tBodyAcc-std()-Y          - the average value of the sampled tBodyAcc-std()-Y value for the given subject and activity             
006 tBodyAcc-std()-Z          - the average value of the sampled tBodyAcc-std()-Z value for the given subject and activity             
041 tGravityAcc-mean()-X      - the average value of the sampled tGravityAcc-mean()-X value for the given subject and activity         
042 tGravityAcc-mean()-Y      - the average value of the sampled tGravityAcc-mean()-Y value for the given subject and activity         
043 tGravityAcc-mean()-Z      - the average value of the sampled tGravityAcc-mean()-Z value for the given subject and activity         
044 tGravityAcc-std()-X       - the average value of the sampled tGravityAcc-std()-X value for the given subject and activity          
045 tGravityAcc-std()-Y       - the average value of the sampled tGravityAcc-std()-Y value for the given subject and activity          
046 tGravityAcc-std()-Z       - the average value of the sampled tGravityAcc-std()-Z value for the given subject and activity          
081 tBodyAccJerk-mean()-X     - the average value of the sampled tBodyAccJerk-mean()-X value for the given subject and activity        
082 tBodyAccJerk-mean()-Y     - the average value of the sampled tBodyAccJerk-mean()-Y value for the given subject and activity        
083 tBodyAccJerk-mean()-Z     - the average value of the sampled tBodyAccJerk-mean()-Z value for the given subject and activity        
084 tBodyAccJerk-std()-X      - the average value of the sampled tBodyAccJerk-std()-X value for the given subject and activity         
085 tBodyAccJerk-std()-Y      - the average value of the sampled tBodyAccJerk-std()-Y value for the given subject and activity         
086 tBodyAccJerk-std()-Z      - the average value of the sampled tBodyAccJerk-std()-Z value for the given subject and activity         
121 tBodyGyro-mean()-X        - the average value of the sampled tBodyGyro-mean()-X value for the given subject and activity           
122 tBodyGyro-mean()-Y        - the average value of the sampled tBodyGyro-mean()-Y value for the given subject and activity           
123 tBodyGyro-mean()-Z        - the average value of the sampled tBodyGyro-mean()-Z value for the given subject and activity           
124 tBodyGyro-std()-X         - the average value of the sampled tBodyGyro-std()-X value for the given subject and activity            
125 tBodyGyro-std()-Y         - the average value of the sampled tBodyGyro-std()-Y value for the given subject and activity            
126 tBodyGyro-std()-Z         - the average value of the sampled tBodyGyro-std()-Z value for the given subject and activity            
161 tBodyGyroJerk-mean()-X    - the average value of the sampled tBodyGyroJerk-mean()-X value for the given subject and activity       
162 tBodyGyroJerk-mean()-Y    - the average value of the sampled tBodyGyroJerk-mean()-Y value for the given subject and activity       
163 tBodyGyroJerk-mean()-Z    - the average value of the sampled tBodyGyroJerk-mean()-Z value for the given subject and activity       
164 tBodyGyroJerk-std()-X     - the average value of the sampled tBodyGyroJerk-std()-X value for the given subject and activity        
165 tBodyGyroJerk-std()-Y     - the average value of the sampled tBodyGyroJerk-std()-Y value for the given subject and activity        
166 tBodyGyroJerk-std()-Z     - the average value of the sampled tBodyGyroJerk-std()-Z value for the given subject and activity        
201 tBodyAccMag-mean()        - the average value of the sampled tBodyAccMag-mean() value for the given subject and activity           
202 tBodyAccMag-std()         - the average value of the sampled tBodyAccMag-std() value for the given subject and activity            
214 tGravityAccMag-mean()     - the average value of the sampled tGravityAccMag-mean() value for the given subject and activity        
215 tGravityAccMag-std()      - the average value of the sampled tGravityAccMag-std() value for the given subject and activity         
227 tBodyAccJerkMag-mean()    - the average value of the sampled tBodyAccJerkMag-mean() value for the given subject and activity       
228 tBodyAccJerkMag-std()     - the average value of the sampled tBodyAccJerkMag-std() value for the given subject and activity        
240 tBodyGyroMag-mean()       - the average value of the sampled tBodyGyroMag-mean() value for the given subject and activity          
241 tBodyGyroMag-std()        - the average value of the sampled tBodyGyroMag-std() value for the given subject and activity           
253 tBodyGyroJerkMag-mean()   - the average value of the sampled tBodyGyroJerkMag-mean() value for the given subject and activity      
254 tBodyGyroJerkMag-std()    - the average value of the sampled tBodyGyroJerkMag-std() value for the given subject and activity       
266 fBodyAcc-mean()-X         - the average value of the sampled fBodyAcc-mean()-X value for the given subject and activity            
267 fBodyAcc-mean()-Y         - the average value of the sampled fBodyAcc-mean()-Y value for the given subject and activity            
268 fBodyAcc-mean()-Z           - the average value of the sampled fBodyAcc-mean()-Z value for the given subject and activity          
269 fBodyAcc-std()-X            - the average value of the sampled fBodyAcc-std()-X value for the given subject and activity           
270 fBodyAcc-std()-Y            - the average value of the sampled fBodyAcc-std()-Y value for the given subject and activity           
271 fBodyAcc-std()-Z            - the average value of the sampled fBodyAcc-std()-Z value for the given subject and activity           
345 fBodyAccJerk-mean()-X       - the average value of the sampled fBodyAccJerk-mean()-X value for the given subject and activity      
346 fBodyAccJerk-mean()-Y       - the average value of the sampled fBodyAccJerk-mean()-Y value for the given subject and activity      
347 fBodyAccJerk-mean()-Z       - the average value of the sampled fBodyAccJerk-mean()-Z value for the given subject and activity      
348 fBodyAccJerk-std()-X        - the average value of the sampled fBodyAccJerk-std()-X value for the given subject and activity       
349 fBodyAccJerk-std()-Y        - the average value of the sampled fBodyAccJerk-std()-Y value for the given subject and activity       
350 fBodyAccJerk-std()-Z        - the average value of the sampled fBodyAccJerk-std()-Z value for the given subject and activity       
424 fBodyGyro-mean()-X          - the average value of the sampled fBodyGyro-mean()-X value for the given subject and activity         
425 fBodyGyro-mean()-Y          - the average value of the sampled fBodyGyro-mean()-Y value for the given subject and activity         
426 fBodyGyro-mean()-Z          - the average value of the sampled fBodyGyro-mean()-Z value for the given subject and activity         
427 fBodyGyro-std()-X           - the average value of the sampled fBodyGyro-std()-X value for the given subject and activity          
428 fBodyGyro-std()-Y           - the average value of the sampled fBodyGyro-std()-Y value for the given subject and activity          
429 fBodyGyro-std()-Z           - the average value of the sampled fBodyGyro-std()-Z value for the given subject and activity          
503 fBodyAccMag-mean()          - the average value of the sampled fBodyAccMag-mean() value for the given subject and activity         
504 fBodyAccMag-std()           - the average value of the sampled fBodyAccMag-std() value for the given subject and activity          
516 fBodyBodyAccJerkMag-mean()  - the average value of the sampled fBodyBodyAccJerkMag-mean() value for the given subject and activity 
517 fBodyBodyAccJerkMag-std()   - the average value of the sampled fBodyBodyAccJerkMag-std() value for the given subject and activity  
529 fBodyBodyGyroMag-mean()     - the average value of the sampled fBodyBodyGyroMag-mean() value for the given subject and activity    
530 fBodyBodyGyroMag-std()      - the average value of the sampled fBodyBodyGyroMag-std() value for the given subject and activity     
542 fBodyBodyGyroJerkMag-mean() - the average value of the sampled fBodyBodyGyroJerkMag-mean() value for the given subject and activity
543 fBodyBodyGyroJerkMag-std()  - the average value of the sampled fBodyBodyGyroJerkMag-std() value for the given subject and activity 
