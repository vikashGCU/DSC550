```python
# Importing libraries
import pandas as pd
from sklearn import tree
from sklearn import preprocessing
import csv
```


```python
# Creating a CSV file with 4 input values
feat =  [
             ["Round","Rough",1.12], # Orange
             ["Elliptical","Smooth",0.47], # Apple
             ["Round","Rough",1.71], # Orange
            ["Round","Rough",1.23]] # Orange

with open('innovators.csv', 'w', newline='') as file:
    writer = csv.writer(file, delimiter='|')
    writer.writerows(data_list)


# Creating a preprocessor function which would transform the input values into 1 or -1
# 1 for Smooth, Round, and >1 pound and -1 for Rough, Elliptical, and <1 pound


def ftr(feat):

    for i in range(len(feat)):
        if feat[i][2] >1:
            feat[i][2]=1
        else:
            feat[i][2]= -1
        
        if feat[i][1] =="Smooth":
            feat[i][1]=1
        else:
            feat[i][1]= -1
        
        if feat[i][0] =="Round":
            feat[i][0]=1
        else:
            feat[i][0]= -1
    return feat

# Created a label corresponding to CSV file input,1 represents orange and 0 represents apple

labels = [1, 0, 1, 1] 



```


```python
# Testing the preprocessor function
print (ftr([["Elliptical","Smooth",0.2]])) # Orange

print (ftr([["Round","Rough",1.2]])) # Apple
```

    [[-1, 1, -1]]
    [[1, -1, 1]]



```python

# Its time to Train classifier, using the DecisionTree classifier

classifier = tree.DecisionTreeClassifier()  # using decision tree classifier

classifier = classifier.fit(ftr(feat), labels)  # Find patterns in data
```


```python
# Created a function which would output which would be understandable 
def pattern(a):
    if classifier.predict(a)==1:
        return "Orange"
    else:
        return "Apple"
```


```python
# Model Testing
# Its time to test the model depending on random input
print(pattern(ftr([["Round","Rough",1.2]])))
print(pattern(ftr([["Elliptical","Smooth",0.2]])))
```

    Orange
    Apple



```python

```
