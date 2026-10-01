At the end of this experiment, the student should be able to filter tabular data using several categorical and numerical conditions, construct focused DataFrames by selecting relevant features, summarize the relationship between categorical features and a numerical variable, and communicate a data comparison using clear and correctly labeled plots.

This experiment uses the <mark>ECE Board Exam 2</mark> as the dataset and will utilize Pandas and a Python plotting library to classify the required dataframes.

```python 
import pandas as pd
```
<mark>Pandas</mark> is utilized to load its functions and an uploaded excel file from the main dataset.
```python
ECE_Board_Exam_2 = pd.read_excel('board2.xlsx') 
ECE_Board_Exam_2
```
<mark>pd.read_excel('board2.xlsx')</mark> this function will import the excel file data to this program and it will be the primary source of data required in each dataframe below

## A. Visayas Communication Dataframe

```python
ECE_Board_Exam_2['Average'] = (ECE_Board_Exam_2['Math'] + ECE_Board_Exam_2['Electronics'] + ECE_Board_Exam_2['GEAS'] + ECE_Board_Exam_2['Communication'])/4
```
The average was not given in the excel file but it can be programmed by getting the mean of each subjects, which can also be used for more programming requirements later in this experiment
```python
VisComm = ECE_Board_Exam_2.loc[(ECE_Board_Exam_2['Hometown']=='Visayas')&(ECE_Board_Exam_2['Track']=='Communication'),
['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm
```
This function will only show the required categories, such that it will only show students whose Hometown is Visayas and whose Track is Communication while only retaining these categories: Name, Gender, Math, Electronics, Average

| | Name |	Gender |	Math |	Electronics |	Average |
| :--- | :--- | :--- | :--- | :--- | :--- | 
| **10** | 	S11 |	Female |	48 |	56 |	54.75 |
| **11** |	S12 |	Male |	89 |	67 |	76.00 |
| **17** |	S18	| Male |	81 |	40 |	63.50 |
| **21** |	S22 |	Female |	64 |	39 |	62.50 |
| **27** |	S28	| Male	| 85 |	53 |	67.75 |


```python
print("Number of rows: ", VisComm.shape[0])
```
This will show the number of rows or the number of students of this dataframe  
```result
Number of rows:  5
```

## B. Visayas Female Dataframe

```python
VisFemale = ECE_Board_Exam_2.loc[(ECE_Board_Exam_2['Hometown']=='Visayas')&(ECE_Board_Exam_2['Gender']=='Female'), 
['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale
```
Similar from the Visayas Communication DataFrame, however this will only display students whose Hometown is Visayas and whose Gender is Female, while retaining only retaining these categories: Name, Track, GEAS, Electronics, Average

| | Name |	Track |	GEAS |	Electronics |	Average |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **5** |	S6 |	Microelectronics |	86 |	45 |	75.50 |
| **10** |	S11 |	Communication |	48 |	56 |	54.75 |
| **20** |	S21 |	Microelectronics |	68 |	51 |	68.50 |
| **21** |	S22 |	Communication |	89 |	39 |	62.50 |
| **23** |	S24 |	Microelectronics |	60 |	45 |	57.75| 
| **25** |	S26 |	Instrumentation |	83 |	47 |	65.75 |

```python
display(VisFemale[VisFemale['Average']>=60])
```
Base from the dataframe of the previous code, this will only display students whose average is 60 and above

| | Name |	Track |	GEAS |	Electronics |	Average |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **5** |	S6 |	Microelectronics |	86 |	45 |	75.50 |
| **20** |	S21 |	Microelectronics |	68 |	51 |	68.50 |
| **21** |	S22 |	Communication |	89 |	39 |	62.50 |
| **25** |	S26 |	Instrumentation |	83 |	47 |	65.75 |


## C. Category-Average Visualization

```python
import matplotlib.pyplot as plt
```
<mark>matplotlib.pyplot</mark> is a library function in Python Programming used to create and display data visualization

```python
Average_Track = ECE_Board_Exam_2.pivot_table(index='Track', values='Average').reset_index()
Average_Track
```
This will display the mean of Average scores of students with the same track

| | Track |	Average |
| :--- | :--- | :--- | 
| **0**	| Communication |	67.975 |
| **1**	| Instrumentation |	65.225 |
| **2** |	Microelectronics |	67.500 |
 
```python
Average_Gender = ECE_Board_Exam_2.pivot_table(index='Gender', values='Average').reset_index()
Average_Gender
```
This will display the mean Average scores of students based on their gender

| | Gender |	Average |
| :--- | :--- | :--- | 
| **0** |	Female |	66.616667 |
| **1** |	Male |	67.183333 |


```python
Average_Hometown = ECE_Board_Exam_2.pivot_table(index='Hometown', values='Average').reset_index()
Average_Hometown
```
This will display the mean Average scores of students based on their hometown


| | Hometown | Average |
| :--- | :--- | :--- | 
| **0** |	Luzon |	68.083333 |
| **1** |	Mindanao |	66.678571 |
| **2** |	Visayas |	65.750000 |


```python
plt.figure(figsize=(15,4))

plt.subplot(1, 3, 1)
plt.bar(Average_Track['Track'], Average_Track['Average'])
plt.title('Average by Track')
plt.xlabel('Track')
plt.ylabel('Average')

plt.subplot(1, 3, 2)
plt.bar(Average_Gender['Gender'], Average_Gender['Average'])
plt.title('Average by Gender')
plt.xlabel('Gender')
plt.ylabel('Average')

plt.subplot(1, 3, 3)
plt.bar(Average_Hometown['Hometown'], Average_Hometown['Average'])
plt.title('Average by Hometown')
plt.xlabel('Hometown')
plt.ylabel('Average')

plt.tight_layout()
```
This will create and visualize a chart based from the previous codes, using the x-axis of the graph as the feature, which are track, gender, and hometown, and the y-axis of the graph as the mean of the averages computed among the students

Below the image of the created chart from this code, are the statements identifying the category with the highest sample mean for each feature
<img width="856" height="227" alt="Screenshot 2026-10-01 071726" src="https://github.com/user-attachments/assets/3373d660-5e6e-429b-98f1-b8d17ae8f2e5" />
##### The highest Average by Track from this DataFrames is Communication, with an average of 67.975
##### The highest Average by Gender from this DataFrames is Male, with an average of 67.183
##### The highest Average by Hometown from this DataFrames is Luzonm, with average of 68.083
