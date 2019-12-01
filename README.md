**KeyStroke-Dynamics** <br/>
Keystroke dynamics refers to the automated method of identifying or confirming the identity of an individual based on the manner and the rhythm of typing on a keyboard. Keystroke dynamics are a powerful behavioral biometric measurement capable of determining user identity and for continuous authentication. It utilizes the manner and rhythm in which each individual types. It is an unobtrusive method that can complement an existing security system such as  password scheme.
<br/>
<br/>
This project tries to verify a subject's identity based on his keystroke patterns, ie, his typing habits.
It is a Python implementation using following 5 models that measure the similarity between a subject's modelled typing behavior and a new typing sample:

Manhattan Distance
Euclidean Distance

The results has been reported as the average EER values on the CMU Keystroke Benchmark dataset. The dataset, in form of a csv and an xls file, has been uploaded in the repo.

Note : Keep all the files in the same folder

**Data Acquisition** <br/>
This project mainly uses two datasets, first dataset is collected by running the ipynb named Collecting keystroke. This file takes input from user and stores it into the collecting_keystroke.csv. The first input is the name of the user and after that the user is asked to enter alphanumeric data with some special characters.<br/>
To get the key stroke dynamics, pyhook python library is used. This library allows to write own event listeners to key up and key down events with the other information such as time, the key id of the key pressed, ascii value of the key pressed etc. [1]. The code overwrites the key Up and key Down event and store the data of username, the ascii value of the key pressed, the event for the key (key up or key down) and the time when the key event happened in milliseconds with reference to the UNIX time.<br/>
The **Second dataset** is called CMU Keystroke Dynamics Benchmark Data-set [2] which comprised of keystroke information for 51 users, each user typing the password “.tie5Roanl” 400 times. The recruited 51 subjects (typists) fully completed the study. All subjects typed the same password, and each subject typed the password 400 times over 8 sessions (50 repetitions per session). The password (.tie5Roanl) was chosen to be representative of a strong 10-character password.
<br/>
**Feature Extraction**<br/>
<br/>To calculate timing features for the first dataset, for each user the key down and key up event for each key id is identified. For the key pressing event, the event of down-up pair is one key stroke. So, from the millisecond value which is stored in collecting keystroke csv file is taken into calculation to find values of Hold, Down-Down and Up-Down. We are considering ascii value of 33 to 122 (a-z A-Z 0-9 and special characters). The values for each key and user combination taken from the input file and then the values are calculated and stored in keystrokedistance.csv.
For second dataset, the raw records of all the subjects' keystrokes and timestamps were analyzed to create a password-timing table. The password-timing containing timings of Hold (H), Down-Down (DD) and Up-Down (UD) is stored in table encodes the timing features for each of the 400 passwords that each subject typed. [3]. The second dataset is stored in keystroke.csv

**Feature Engineering**
<br/>After having all the dataset timing values, now the project will train the model using this data. We have used Manhattan, Euclidean and K-means algorithmic models. We take both the dataset as input to the algorithm and divide the dataset into 70-30% for training and testing datasets. The training data is applied to each algorithm and the test data is used to predict if the model can predict the user is valid or not. These models are written in the file named analysis ipynb.<br/>

For Manhattan and Euclidean algorithm, we consider mean vector for the training dataset and using that we are generating distance between the testing dataset and the mean value using python function called city block and Euclidean to calculate the both distances respectively. For K-means, The dataset only uses the timing variables and we apply K-means algorithm for n=5 which uses predict method of GridSearchCV python package.<br/>

**Result**<br/>
The result here is compared in the form of ROC curve. There were two datasets in which one was controlled, and another is self-collected gibberish dataset. The three models which are applied are Manhattan distance, Euclidean distance and k-means algorithm. The comparison of equal error rate (ERR) is shown below in the table.

<br/>https://appliedmachinelearning.wordpress.com/2017/01/23/nlp-blog-post/

<br/>
All the results are in: <br/> Report_KeyStrokeDynamics.pdf<br/>
KeyStroke Dynamics for user authentication.pptx
