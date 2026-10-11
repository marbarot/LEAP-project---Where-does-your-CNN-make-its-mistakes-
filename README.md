# LEAP-project---CNN-classification-

## 1. Project description
This portfolio consists of the final project for the LEAP Machine Learning with Python course. The main focus is to employ a convolutional neural network (CNN) that recognizes handwritten digits, identifying misclassifications and applying an architectural change to improve the model's pattern recognition.

## 2. Problem statement
In this project, the goal is to create a model that accurately predicts handwritten numbers and can be employed to support automation in postal sorting centers and bank transactions. Such high-stakes situations, where a misinterpretation of a single digit carries significant cost, demand for high accuracy, as well as error interpretation. Hence, a main objective is to understand where the errors are made so that they are identified early on during the procedures. 

## 3. Data set
The MNIST dataset is utilized, downloaded via OpenML. It contains 70,000 images of handwritten digits (labeled 0 through 9). Each input represents a 28 by 28 pixel bounding box in grayscale.

## 4. Method
*Preprocessing* 
Each of the flat rows consisting of 784 numbers was reshaped back into 28x28x1 image matrices.
Normalization was performed by scaling pixel values from 0-255 down to 0-1.
Stratified split was utilized to divide the data into training and testing sets.

*Model*
a. *Model1* A sequential CNN was employed, with a `Conv2D` layer (32 filters), `MaxPooling2D`, `Dropout` (0.3), flattening, and a `Dense` hidden layer.
b. *Model2* A deeper architecture was created featuring a second `Conv2D` (64 filters) and `MaxPooling2D` block prior to flattening to better capture complex spatial features.

In both models `sparse_categorical_crossentropy` loss and `EarlyStopping` were utilized (monitoring validation loss with a patience of 3). 

## 5. Results
The first CNN model yielded a test accuracy of 98.59%. Analyzing the confusion matrix  revealed that the model misinterpreted true 4s as 9s (in 17 instances) and true 9s as 7s (in 10 instances). These digits' shapes appear to be visually similar. 

The overall test accuracy was elevated to 99.06% when implementing the deeper architecture. Additionally, an important highlight is that the second model successfully reduced the errors, with 4s misclassified as 9s dropping to 9 instances, and 9s misclassified as 7s dropping to 3 instances.

## 6. Interpretation
The second model with deeper architecture successfully reduced the errors by about half, which indicates that it managed to capture more complex spatial relationships. This allowed for the distinction of curved rather than sharp lines. 
However, deploying such a model in real-world settings carries ethical risks. Specifically, it was trained on a dataset that may under-represent the handwriting of several subgroups of people, including foreigners, varying age groups and people of different educational backgrounds. Hence, in high-stakes settings, this could result in discrimination, alongside the administrative burden on specific demographics demanding the constant correction of automated errors.

## 7. Reflection
Not relying solely on the accuracy metric, but also analyzing the confusion matrices was highly important for understanding the model's performance and weaknesses. Identifying the reason why those visually similar digits were confused guided the selection of the right architectural fix. 
For future work, several improvements could be implemented. In particular, exploring explainability techniques could provide a better understanding of the network's decision-making process. Neural networks are often considered "black boxes", hence it would provide valuable insight on the errors produced. Additionally, data augmentation for the introduction of more varied handwriting styles would make the model more robust against the demographic bias identified in the ethical analysis.
