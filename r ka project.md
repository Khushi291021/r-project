# Student Score Analysis in R 
 
# Sample dataset: Student names and their scores in 3 subjects student_data <- data.frame( 
  Name = c("Alice", "Bob", "Charlie", "Diana", "Ethan", "Fiona", "George", "Hannah", "Ian", "Julia"), 
  Math = c(85, 78, 92, 67, 88, 73, 95, 80, 60, 77), 
  Science = c(90, 82, 88, 70, 85, 75, 93, 78, 65, 80), 
  English = c(78, 85, 80, 72, 90, 70, 88, 76, 68, 82) 
) 
 
# Display the student score table print("Student Scores:") print(student_data) 
 
# Summary Statistics 
 
summary_stats <- function(subject_scores) {   list( 
    Mean = mean(subject_scores), 
    Median = median(subject_scores), 
    Std_Dev = sd(subject_scores) 
  ) 
} 
 
subjects <- c("Math", "Science", "English") 
 
cat("\nSummary Statistics:\n") for (subject in subjects) {   cat("\n", subject, ":\n")   print(summary_stats(student_data[[subject]])) 
} 
 
# Visualization # Load necessary library if(!require(ggplot2)) install.packages("ggplot2", dependencies=TRUE) library(ggplot2) 
 
# Bar Plot: Student scores by subject student_long <- reshape2::melt(student_data, id.vars = "Name") ggplot(student_long, aes(x = Name, y = value, fill = variable)) +   geom_bar(stat = "identity", position = "dodge") + 
  labs(title = "Student Scores by Subject", x = "Student", y = "Score") +   theme_minimal() 
 
# Box Plot: Score distribution by subject ggplot(student_long, aes(x = variable, y = value, fill = variable)) +   geom_boxplot() +   labs(title = "Box Plot of Scores by Subject", x = "Subject", y = "Score") +   theme_minimal() 
 
# Histogram: Distribution of scores in Math ggplot(student_data, aes(x = Math)) +   geom_histogram(binwidth = 5, fill = "skyblue", color = "black") +   labs(title = "Distribution of Math Scores", x = "Score", y = "Count") +   theme_minimal() 
# Bonus Features 
 
 
# Highest and lowest scorers in each subject cat("\nTop and Bottom Scorers:\n") for (subject in subjects) {   highest <- student_data$Name[which.max(student_data[[subject]])]   lowest <- student_data$Name[which.min(student_data[[subject]])]   cat(subject, " - Highest:", highest, ", Lowest:", lowest, "\n") 
} 
 
# Performance trend across subjects avg_scores <- colMeans(student_data[subjects]) barplot(avg_scores,         main = "Average Scores by Subject", 
        col = c("tomato", "gold", "skyblue"),         ylab = "Average Score") 
