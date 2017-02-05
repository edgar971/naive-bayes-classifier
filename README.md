___
**Implementing Naive-Bayes Classifier for the dataset *tennis.csv* along with Laplacian smoothing**
___
* Libraries imported : `pandas`

* Class Description: We have a class named `Classifier()` where the constructor takes 3 parameters: 

```python
def __init__(self,filename = None, class_attr = None, k = 1.0):
```
1. `filename` is our file *tennis.csv*
2. k is the value inputted for Additive smoothing or Laplacian smoothing
3. `class_attr` is the attribute on which we perform Naive-Bayes. In this case, `class_attr` is the 'Play' column from our dataset.


We have a method called `def calculate_prior(self)` which calculates the prior probablities for the class attribute i.e. `Play`, where

        probability(class) =    How many  times it appears in column
                             __________________________________________
                                  count of all class attribute

Next we have a method called `def set_sizes(self)`. This just sets the total number of distinct row under any attribute to a dictionary called `sizes{}`. 

Next we have a method called `get_cp(self, attr, attr_type, class_value)`, where we calculate the conditional probability for the given constraints. This function prints and retuurns the required conditional probablity.`k` is the required laplacian constant.                                             

       
    P(attr = attr_type|class_data = class_value) =
    											k + P(attr_type ∩ class_value)
                             		 	 ________________________________________________
                              	            k.(size of distinct attr) + P(class_value)
                                                    
After `get_cp`, we have a function called `calculate_conditional_probabilities(self, hypothesis)` which just multiplies the probabilities calculated in the previous function. Here we calculate **Likelihood** of Evidence by multiplying all individual probabilities with their prior probabilities 
        
  	(Outcome|Multiple Evidence) = P(Evidence1|Outcome) x P(Evidence2|outcome) 
  									    	x ... x P(EvidenceN|outcome) x P(Outcome)

At last, we have a classifying called `classify(self)` which is calls all the required methods and prints the outcome. 


* __main__ starts by printing the prior probablities and the sizes of all the attributes. Then it asks the value of `k` for laplacian smoothing. The user is to input the conditions : 
	1. Outlook : sunny/overcast/rainy
	2. Temperature : hot/mild/cool
	3. Humidity : high/normal
	4. Windy? : true/false

After the input, an object is initialsed and the functions are called resulting in an output like this: 

```sh
~ desktop$ python nb_1.py

	Welcome to the naive bayes classifying program for tennis.csv

Please enter the value of 'k' for Laplacian smoothing: 1
The prior probabilities for 'yes' and 'no' in the 'Play' column are:
{'no': 0.35714285714285715, 'yes': 0.6428571428571429}

The sizes of the rest of the attribute columns are: 
{'Outlook': 3, 'Temp.': 3, 'Play': 2, 'Humidity': 2, 'Windy': 2}

Provide conditions for Outlook (sunny/overcast/rainy): 
Provide conditions for temperature (hot/mild/cool): 
Provide conditions for humidity (high/normal): 
Is it windy? (true/false): 

The conditional probabilities are as follows:
P ( Outlook =  | Play =  no ) = ( 1 + 1.0 ) / ( 3 + 1.0 * 5.0 ) =  0.125
P ( Temp. =  | Play =  no ) = ( 1 + 1.0 ) / ( 3 + 1.0 * 5.0 ) =  0.125
P ( Humidity =  | Play =  no ) = ( 1 + 1.0 ) / ( 2 + 1.0 * 5.0 ) =  0.14285714285714285
P ( Windy =  | Play =  no ) = ( 1 + 1.0 ) / ( 2 + 1.0 * 5.0 ) =  0.14285714285714285
P ( Outlook =  | Play =  yes ) = ( 1 + 1.0 ) / ( 3 + 1.0 * 9.0 ) =  0.08333333333333333
P ( Temp. =  | Play =  yes ) = ( 1 + 1.0 ) / ( 3 + 1.0 * 9.0 ) =  0.08333333333333333
P ( Humidity =  | Play =  yes ) = ( 1 + 1.0 ) / ( 2 + 1.0 * 9.0 ) =  0.09090909090909091
P ( Windy =  | Play =  yes ) = ( 1 + 1.0 ) / ( 2 + 1.0 * 9.0 ) =  0.09090909090909091

Result with Laplacian smoothing:
no  -->  0.05102040816326531
yes  -->  0.05844155844155845

