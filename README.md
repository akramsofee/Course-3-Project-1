# Course-3-Project-1
Course 3 (Getting &amp; Cleaning Data), Course Project 1 of 1
##Assign tables as objects
of the form:
activity_labels <- read.table("UCI HAR Dataset/activity_labels.txt")

##Combine tables 
x.all <- rbind(x_test,x_train)

y.all <- rbind(y_test,y_train)

subject.all <- rbind(subject_test,subject_train)

##Replace column names 
data_labels = sapply(features$V2, function(x) {gsub('[-(),]+','_',x)})

colnames(x.all) <- data_labels

##Retain only desired information 
features_mean_and_std <- grep('mean|std', features$V2, ignore.case = TRUE)

x.all <- x.all[,features_mean_and_std]

for (i in 1:6) {
+ x.all$activity[y.all$V1 ==i ] <- as.character(activity_labels[i,2])
+ }
subject.all <- rbind(subject_test,subject_train)
x.all$subject <- as.factor(subject.all$V1)

##Aggregate data 
tidy <- aggregate(. ~ subject+activity, data = x.all, FUN = mean)
##Save table in desired form
write.table(tidy, "tidy.txt", sep = "\t")
