# KeyStrokeDyamics
User Verification based on Keystroke Dynamics

 A program to **collect keystroke data, refactor it and analyze it by applying different algorithm model**

In Collbration with [Urvi Sheth](https://github.com/urvisheth) and Aditya Yaji


## Steps to execute
1. Execute **Collecting key stroke.ipynb** , enter name, press enter and then enter alphanumeric data on which you want keystroke data. See the stored data in Collecting_keyStroke.csv

2. After 1, execute **calculatingValues.ipynb** , this will generate derived values from the previous csv. New Values are stored in, **KeyStrokeDistance.csv**

3. execute **Analysis.ipynb** to see the analysis for both the datasets for the three algorithms mentioned below. 


## Proposal

In the project, we will verify the identity of users on the basis of the keystroke information. 
A model will be first trained by providing it with the typing patterns of the users to be enrolled, multiple patterns per user. 
The model is then provided with test patterns from the user as well as others posing as that user.  The model should be able to reject the imposters while accept the genuine user based on the test pattern similarity to the trained model for the user. 
We will test various detectors which provide different ways of measuring this similarity.
Manhattan Distance
Euclidean Distance
K-Nearest Neighbours

## Implementation 
The implementation for generating key stroke dynamics and model training is done is three phases in this project using python 3.6/3.7:

•	Data Acquisition

•	Feature Extraction

•	Feature Engineering

### Data Acquisition - Datasets

#### Dataset 1

This project mainly uses two datasets, first dataset is collected by running the ipynb named Collecting keystroke. This file takes input from user and stores it into the collecting_keystroke.csv. The first input is the name of the user and after that the user is asked to enter alphanumeric data with some special characters.
To get the key stroke dynamics, pyhook python library is used. This library allows to write own event listeners to key up and key down events with the other information such as time, the key id of the key pressed, ascii value of the key pressed etc.

![keystroke Image](https://github.com/urvisheth/KeyStrokeDyamics/raw/master/image/op1.png "Input 1 example")

#### Dataset -2

The Second dataset is called CMU Keystroke Dynamics Benchmark Data-set [2] which comprised of keystroke information for 51 users, each user typing the password “.tie5Roanl” 400 times. The recruited 51 subjects (typists) fully completed the study. All subjects typed the same password, and each subject typed the password 400 times over 8 sessions (50 repetitions per session). The password (.tie5Roanl) was chosen to be representative of a strong 10-character password [1].

![keystroke Image](https://github.com/urvisheth/KeyStrokeDyamics/blob/master/image/key.png)

### Feature Extraction

#### For Dataset - 1 

To calculate timing features for the first dataset, for each user the key down and key up event for each key id is identified. For the key pressing event, the event of down-up pair is one key stroke. So, from the millisecond value which is stored in collecting keystroke csv file is taken into calculation to find values of Hold, Down-Down and Up-Down. We are considering ascii value of 33 to 122 (a-z A-Z 0-9 and special characters). The values for each key and user combination taken from the input file and then the values are calculated and stored in keystrokedistance.csv.

![keystroke Image](https://github.com/urvisheth/KeyStrokeDyamics/raw/master/image/op2.png "Input 2")


#### For Dataset - 2

For second dataset, the raw records of all the subjects' keystrokes and timestamps were analyzed to create a password-timing table. The password-timing containing timings of Hold (H), Down-Down (DD) and Up-Down (UD) is stored in table encodes the timing features for each of the 400 passwords that each subject typed. [1]. The second dataset is stored in keystroke.csv

### Feature Engineering

After having all the dataset timing values, now the project will train the model using this data. We have used Manhattan, Euclidean and K-means algorithmic models. We take both the dataset as input to the algorithm and divide the dataset into 70-30% for training and testing datasets. The training data is applied to each algorithm and the test data is used to predict if the model can predict the user is valid or not. These models are written in the file named analysis ipynb. 

## Results

The result here is compared in the form of ROC curve. There were two datasets in which one was controlled, and another is self-collected gibberish dataset. The three models which are applied are Manhattan distance, Euclidean distance and k-means algorithm. 

Though the error rate seems bad in comparison, it is still a better result as it gives minimum of 55-60% accuracy for the worst case.

![keystroke Image](https://github.com/urvisheth/KeyStrokeDyamics/raw/master/image/op3.png "set 3")


The comparison of equal error rate (ERR) is shown below in the table.



| Methods	   |    Equal Error rate   |                 |
|------------|:---------------------:| ---------------:|
|            |         Dataset 1     |   Dataset 2	    |
|Manhattan   |          0.383        |	     0.195      |
|Euclidean   |          0.444	       |	     0.218	     |
|K-Means     |         `0.306`	      |     `0.155`     |

## References

[1] http://www.cs.cmu.edu/~keystroke/

[2] https://appliedmachinelearning.blog/2017/07/26/user-verification-based-on-keystroke-dynamics-python-code/

[3] https://github.com/njanakiev/keystroke-biometrics/blob/master/keystroke-biometrics.ipynb

[4] https://github.com/abhijeet3922/User-Verification-based-on-Keystroke-Dynamics
