# School_District_Analysis
The purpose of the analysis is to find the overall passing percentages of students and determine if there is any correlation with the budget per student using numpy-python.

### Import required dependencies


```python
import pandas as pd
import os
```

## Deliverable 1: Collect the Data

To collect the data that you’ll need, complete the following steps:

1. Using the Pandas `read_csv` function and the `os` module, import the data from the `new_full_student_data.csv` file, and create a DataFrame called student_df. 

2. Use the head function to confirm that Pandas properly imported the data.



```python
# Create the path and import the data
full_student_data = os.path.join('../Resources/new_full_student_data.csv')
student_df = pd.read_csv(full_student_data)
```


```python
# Verify that the data was properly imported
student_df.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>student_name</th>
      <th>grade</th>
      <th>school_name</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>school_type</th>
      <th>school_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>103880842</td>
      <td>Travis Martin</td>
      <td>9th</td>
      <td>Sullivan High School</td>
      <td>59.0</td>
      <td>88.2</td>
      <td>Public</td>
      <td>961125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45069750</td>
      <td>Michael Brown</td>
      <td>9th</td>
      <td>Dixon High School</td>
      <td>94.7</td>
      <td>73.5</td>
      <td>Charter</td>
      <td>870334</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45024902</td>
      <td>Gabriela Lucero</td>
      <td>9th</td>
      <td>Wagner High School</td>
      <td>89.0</td>
      <td>70.4</td>
      <td>Public</td>
      <td>846745</td>
    </tr>
    <tr>
      <th>3</th>
      <td>62582498</td>
      <td>Susan Richardson</td>
      <td>9th</td>
      <td>Silva High School</td>
      <td>69.7</td>
      <td>80.3</td>
      <td>Public</td>
      <td>991918</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16437227</td>
      <td>Sherry Davis</td>
      <td>11th</td>
      <td>Bowers High School</td>
      <td>NaN</td>
      <td>27.5</td>
      <td>Public</td>
      <td>848324</td>
    </tr>
  </tbody>
</table>
</div>



## Deliverable 2: Prepare the Data

To prepare and clean your data for analysis, complete the following steps:
    
1. Check for and remove all rows with `NaN`, or missing, values in the student DataFrame. 

2. Check for and remove all duplicate rows in the student DataFrame.

3. Use the `str.replace` function to remove the "th" from the grade levels in the grade column.

4. Check data types using the `dtypes` property.

5. Remove the "th" suffix from every value in the grade column using `str` and `replace`.

6. Change the grade colum to the `int` type and verify column types.

7. Use the head (and/or the tail) function to preview the DataFrame.


```python
# Check for null values
student_df.isnull().sum()
```




    student_id          0
    student_name        0
    grade               0
    school_name         0
    reading_score    1968
    math_score        982
    school_type         0
    school_budget       0
    dtype: int64




```python
# Drop rows with null values and verify removal
student_df = student_df.dropna()
student_df.isnull().sum()
```




    student_id       0
    student_name     0
    grade            0
    school_name      0
    reading_score    0
    math_score       0
    school_type      0
    school_budget    0
    dtype: int64




```python
# Check for duplicated rows
student_df.duplicated().sum()
```




    1836




```python
# Drop duplicated rows and verify removal
# Drop duplicate rows
student_df = student_df.drop_duplicates()
student_df.duplicated().sum()
```




    0




```python
# Check data types
student_df.dtypes
```




    student_id         int64
    student_name      object
    grade             object
    school_name       object
    reading_score    float64
    math_score       float64
    school_type       object
    school_budget      int64
    dtype: object




```python
# Examine the grade column to understand why it is not an int
student_df["grade"]
```




    0         9th
    1         9th
    2         9th
    3         9th
    5         9th
             ... 
    19508    10th
    19509    12th
    19511    11th
    19512    11th
    19513    12th
    Name: grade, Length: 14831, dtype: object




```python
# Remove the non-numeric characters and verify the contents of the column
student_df['grade'] = student_df['grade'].str.replace('th', '')
```


```python
# Change the grade column to the int type and verify column types
student_df["grade"] = student_df["grade"].astype("int")
student_df.dtypes
```




    student_id         int64
    student_name      object
    grade              int64
    school_name       object
    reading_score    float64
    math_score       float64
    school_type       object
    school_budget      int64
    dtype: object



## Deliverable 3: Summarize the Data

Describe the data using summary statistics on the data as a whole and on individual columns.

1. Generate the summary statistics for each DataFrame by using the `describe` function.

2. Display the mean math score using the `mean` function. 

2. Store the minimum reading score as `min_reading_score`.


```python
# Display summary statistics for the DataFrame
student_df.describe()
```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>school_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1.483100e+04</td>
      <td>14831.000000</td>
      <td>14831.000000</td>
      <td>14831.000000</td>
      <td>14831.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>6.975296e+07</td>
      <td>10.355539</td>
      <td>72.357865</td>
      <td>64.675733</td>
      <td>893742.749107</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.452909e+07</td>
      <td>1.097728</td>
      <td>15.224590</td>
      <td>15.844093</td>
      <td>53938.066467</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000906e+07</td>
      <td>9.000000</td>
      <td>10.500000</td>
      <td>3.700000</td>
      <td>817615.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3.984433e+07</td>
      <td>9.000000</td>
      <td>62.200000</td>
      <td>54.500000</td>
      <td>846745.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.965978e+07</td>
      <td>10.000000</td>
      <td>73.800000</td>
      <td>65.300000</td>
      <td>893368.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>9.927449e+07</td>
      <td>11.000000</td>
      <td>84.000000</td>
      <td>76.000000</td>
      <td>956438.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.299997e+08</td>
      <td>12.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>991918.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Display the mean math score using the mean function
avg_math = student_df["math_score"].mean()
print("The mean math score is: " + str(round(avg_math, 2)))
```

    The mean math score is: 64.68



```python
# Store the minimum reading score as min_reading_score
min_reading_score = student_df["reading_score"].min()
print("The minimum reading score is: " + str(min_reading_score))
```

    The minimum reading score is: 10.5


## Deliverable 4: Drill Down into the Data

Drill down to specific rows, columns, and subsets of the data.

To drill down into the data, complete the following steps:

1. Use `loc` to display the grade column.

2. Use `iloc` to display the first 3 rows and columns 3, 4, and 5.

3. Show the rows for grade nine using `loc`.

4. Store the row with the minimum overall reading score as `min_reading_row` using `loc` and the `min_reading_score` found in Deliverable 3.

5. Find the reading scores for the school and grade from the output of step three using `loc` with multiple conditional statements.

6. Using conditional statements and `loc` or `iloc`, find the mean reading score for all students in grades 11 and 12 combined.


```python
# Use loc to display the grade column
student_df.loc[:,["grade"]]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>9</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>19508</th>
      <td>10</td>
    </tr>
    <tr>
      <th>19509</th>
      <td>12</td>
    </tr>
    <tr>
      <th>19511</th>
      <td>11</td>
    </tr>
    <tr>
      <th>19512</th>
      <td>11</td>
    </tr>
    <tr>
      <th>19513</th>
      <td>12</td>
    </tr>
  </tbody>
</table>
<p>14831 rows × 1 columns</p>
</div>




```python
# Use `iloc` to display the first 3 rows and columns 3, 4, and 5.
student_df.iloc[:3]
```



<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>student_name</th>
      <th>grade</th>
      <th>school_name</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>school_type</th>
      <th>school_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>103880842</td>
      <td>Travis Martin</td>
      <td>9</td>
      <td>Sullivan High School</td>
      <td>59.0</td>
      <td>88.2</td>
      <td>Public</td>
      <td>961125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45069750</td>
      <td>Michael Brown</td>
      <td>9</td>
      <td>Dixon High School</td>
      <td>94.7</td>
      <td>73.5</td>
      <td>Charter</td>
      <td>870334</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45024902</td>
      <td>Gabriela Lucero</td>
      <td>9</td>
      <td>Wagner High School</td>
      <td>89.0</td>
      <td>70.4</td>
      <td>Public</td>
      <td>846745</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select the rows for grade nine and display their summary statistics using `loc` and `describe`.
grade9_scores_df = student_df.loc[student_df["grade"] == 9]
grade9_scores_df.describe()
```

<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>school_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4.132000e+03</td>
      <td>4132.0</td>
      <td>4132.000000</td>
      <td>4132.000000</td>
      <td>4132.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>6.979441e+07</td>
      <td>9.0</td>
      <td>69.236713</td>
      <td>66.585624</td>
      <td>898692.606002</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.470565e+07</td>
      <td>0.0</td>
      <td>15.277354</td>
      <td>16.661533</td>
      <td>54891.596611</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000906e+07</td>
      <td>9.0</td>
      <td>17.900000</td>
      <td>5.300000</td>
      <td>817615.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3.953848e+07</td>
      <td>9.0</td>
      <td>59.000000</td>
      <td>56.000000</td>
      <td>846745.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.984037e+07</td>
      <td>9.0</td>
      <td>70.050000</td>
      <td>67.800000</td>
      <td>893368.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>9.939504e+07</td>
      <td>9.0</td>
      <td>80.500000</td>
      <td>78.500000</td>
      <td>957299.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.299997e+08</td>
      <td>9.0</td>
      <td>99.900000</td>
      <td>100.000000</td>
      <td>991918.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Store the row with the minimum overall reading score as `min_reading_row`
# using `loc` and the `min_reading_score` found in Deliverable 3.
min_reading_row = student_df["reading_score"].min()
student_df.loc[student_df["reading_score"] == min_reading_row]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>student_name</th>
      <th>grade</th>
      <th>school_name</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>school_type</th>
      <th>school_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3706</th>
      <td>81758630</td>
      <td>Matthew Thomas</td>
      <td>10</td>
      <td>Dixon High School</td>
      <td>10.5</td>
      <td>58.4</td>
      <td>Charter</td>
      <td>870334</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Use loc with conditionals to select all reading scores from 10th graders at Dixon High School.
tenth_grade_df = (student_df["grade"] == 10) & (student_df["school_name"] == "Dixon High School")

student_df.loc[tenth_grade_df, ["reading_score"]]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>reading_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>45</th>
      <td>71.10</td>
    </tr>
    <tr>
      <th>60</th>
      <td>59.50</td>
    </tr>
    <tr>
      <th>69</th>
      <td>88.60</td>
    </tr>
    <tr>
      <th>94</th>
      <td>81.50</td>
    </tr>
    <tr>
      <th>100</th>
      <td>95.30</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>19283</th>
      <td>52.90</td>
    </tr>
    <tr>
      <th>19306</th>
      <td>58</td>
    </tr>
    <tr>
      <th>19344</th>
      <td>38</td>
    </tr>
    <tr>
      <th>19368</th>
      <td>84.40</td>
    </tr>
    <tr>
      <th>19445</th>
      <td>43.90</td>
    </tr>
  </tbody>
</table>
<p>569 rows × 1 columns</p>
</div>




```python
# Find the mean reading score for all students in grades 11 and 12 combined.

mean_score = student_df.loc[(student_df["grade"] == 11) | (student_df["grade"] == 12), "reading_score"].mean()
print("The mean of all 11th and 12th grade reading scores are " + str(round(mean_score,2)))
```

    The mean of all 11th and 12th grade reading scores is 74.9


## Deliverable 5: Make Comparisons Between District and Charter Schools

Compare district vs charter schools for budget, size, and scores.

Make comparisons within your data by completing the following steps:

1. Using the `groupby` and `mean` functions, look at the average reading and math scores per school type.

1. Using the `groupby` and `count` functions, find the total number of students at each school.

2. Using the `groupby` and `mean` functions, find the average budget per grade for each school type.


```python
# Use groupby and mean to find the average reading and math scores for each school type.
mean_scores_type = student_df.groupby("school_type").mean()
mean_scores_type.loc[:, ["math_score", "reading_score"]]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>math_score</th>
      <th>reading_score</th>
    </tr>
    <tr>
      <th>school_type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>66.761883</td>
      <td>72.450603</td>
    </tr>
    <tr>
      <th>Public</th>
      <td>62.951576</td>
      <td>72.281219</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Display the average budget for each school type by using the groupby and mean functions
avg_budget = student_df.groupby("school_type").mean()
avg_budget.loc[:, ["school_budget"]]
```

<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_budget</th>
    </tr>
    <tr>
      <th>school_type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>872,625.66</td>
    </tr>
    <tr>
      <th>Public</th>
      <td>911,195.56</td>
    </tr>
  </tbody>
</table>
</div>


```python
# Use the `groupby`, `count`, and `sort_values` functions to find the
# total number of students at each school and sort from most students to least students.

school_count = student_df.groupby(by ="school_name").count()
school_count = school_count.sort_values("student_id", ascending = False)
school_count = school_count.rename(columns = {"student_id": "student_count"})
school_count = school_count.loc[:,["student_count"]]
school_count
```

<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_count</th>
    </tr>
    <tr>
      <th>school_name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Montgomery High School</th>
      <td>2038</td>
    </tr>
    <tr>
      <th>Green High School</th>
      <td>1961</td>
    </tr>
    <tr>
      <th>Dixon High School</th>
      <td>1583</td>
    </tr>
    <tr>
      <th>Wagner High School</th>
      <td>1541</td>
    </tr>
    <tr>
      <th>Silva High School</th>
      <td>1109</td>
    </tr>
    <tr>
      <th>Woods High School</th>
      <td>1052</td>
    </tr>
    <tr>
      <th>Sullivan High School</th>
      <td>971</td>
    </tr>
    <tr>
      <th>Turner High School</th>
      <td>846</td>
    </tr>
    <tr>
      <th>Bowers High School</th>
      <td>803</td>
    </tr>
    <tr>
      <th>Fisher High School</th>
      <td>798</td>
    </tr>
    <tr>
      <th>Richard High School</th>
      <td>551</td>
    </tr>
    <tr>
      <th>Campos High School</th>
      <td>541</td>
    </tr>
    <tr>
      <th>Odonnell High School</th>
      <td>459</td>
    </tr>
    <tr>
      <th>Campbell High School</th>
      <td>407</td>
    </tr>
    <tr>
      <th>Chang High School</th>
      <td>171</td>
    </tr>
  </tbody>
</table>
</div>


```python
#Find the average math score by grade for each school type by using the groupby and 
# mean functions, as the following image shows:
by_school_type = student_df.groupby(["school_type", "grade"]).mean()
by_school_type = by_school_type.loc[:, ["math_score"]]
by_school_type.round({"math_score": 1})

```

<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>school_type</th>
      <th>grade</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">Charter</th>
      <th>9</th>
      <td>70.1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>66.4</td>
    </tr>
    <tr>
      <th>11</th>
      <td>68.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>60.2</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Public</th>
      <th>9</th>
      <td>63.8</td>
    </tr>
    <tr>
      <th>10</th>
      <td>63.8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>59.3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>63.6</td>
    </tr>
  </tbody>
</table>
</div>


```python

```

# Deliverable 6: Summarize Your Findings

The goal of analyzing the school data was most likely to discover what variables have the most impact on student's test scores.

Overview:
There were a total of 15 high schools analyzed. All 9-12 grades were tested for both reading and math. There were two different types of schools, charter and public. Lots of missing scores, the reading score had the most with 1968 and the math score was missing 982 scores. 
 
Results:
Reading score (72) average was higher than the Math score average (65). The data had a normal distribution for both math and reading scores (mean was close to median). There were similar scores between the public and charter schools for both reading and math scores. Both public and charter had a mean of 72 for reading scores. The mean for math scores was 62 for public and 66 for charter. Surprisingly, public schools have an average school budget higher (~911,000) than charter schools (~873,000). However, the school budgets are similar. So, most likely school type and school budgets are not factors in test results. Montgomery HS had the largest population of students with 2038 and Chang HS had the lowest with 171. However, since each schools performance on math and reading have not been analyzed, we do not know if school size impacts test scores or not. 

Recommendations:
It would be worthwhile to compare each school's budget and average scores to seem if budgets make an impact on scores. Also, compare school counts with the average scores, possibly the size of the student body effects scores. It would be interesting to know if all grades take the same test every year and if so is there an improvement over time. 
