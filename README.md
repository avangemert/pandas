
# Heroes of Pymoli Data Analysis

- Almost half of players are in the 20-24 age demographic (45.20%). Game marketers should focus on this demographic.
- Although women only make up about one-fifth of players (17.45%), their lifetime spend is almost equal to male players at 3.83 for women and 4.02 for men.
- The most profitable items are game weapons with names such as Retribution Axe, Spectral Diamond Doomblade, and Singed Scalpel.


```python
# Import dependencies

import pandas as pd
pd.options.display.float_format = '${:,.2f}'.format
import numpy as np
```


```python
# Make a reference to the purchase_data.json file path
json_path = "purchase_data.json"

# Import the purchase_data.json file as a DataFrame
purchase_data_df = pd.read_json(json_path, encoding="utf-8")
purchase_data_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>$3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>$2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>$2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>$1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#count players
playerCount = purchase_data_df['SN'].value_counts().count()
print("Total player count: " + str(playerCount) + " players")
```

    Total player count: 573 players



```python
player_count = pd.DataFrame([{"Total Players": playerCount}])
player_count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
#purchasing analysis

uniqueItems = purchase_data_df['Item ID'].value_counts().count()
print("Number of unique items: " + str(uniqueItems))
```

    Number of unique items: 183



```python
# Average Purchase Price

avgPurchasePrice = round(purchase_data_df['Price'].mean(),2)
print("Average purchase price: "+"${:,.2f}".format(avgPurchasePrice))
```

    Average purchase price: $2.93



```python
# Total Number of Purchases

totalPurchases = purchase_data_df['Item ID'].count()
print("Total # of purchases: "+ str(totalPurchases))
```

    Total # of purchases: 780



```python
# Total Revenue

totalRev = round(purchase_data_df['Price'].sum(),2)
print("Total Revenue: "+"${:,.2f}".format(totalRev))
```

    Total Revenue: $2,286.33



```python
# Purchasing Analysis Total

raw_purchasing_data = ([{"Number of Unique Items": "183", "Average Price": '$2.93',
     "Number of Purchases": "780", "Total Revenue": "$2,286.33"}])

purchasing_analysis_df = pd.DataFrame(raw_purchasing_data)
purchasing_analysis_df

purchasing_analysis_df_org = purchasing_analysis_df[["Number of Unique Items", "Average Price", 
                                                     "Number of Purchases", "Total Revenue"]]
purchasing_analysis_df_org
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2,286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Percentage and Count of Male Players

maleCount = purchase_data_df.loc[purchase_data_df["Gender"] == 'Male', :]
malePlayerCount = maleCount['SN'].value_counts().count()
print("Male player count: "+ str(malePlayerCount))

malePercentage = malePlayerCount/playerCount
print("Percentage of male players: "+"{:.2%}".format(malePercentage))
```

    Male player count: 465
    Percentage of male players: 81.15%



```python
# Percentage and Count of Female Players

femaleCount = purchase_data_df.loc[purchase_data_df["Gender"] == 'Female', :]
femalePlayerCount = femaleCount['SN'].value_counts().count()
print("Female player count: "+ str(femalePlayerCount))

avgFemalePercentage = femalePlayerCount/playerCount
print("Percentage of male players: "+"{:.2%}".format(avgFemalePercentage))


```

    Female player count: 100
    Percentage of male players: 17.45%



```python
# Percentage and Count of Other / Non-Disclosed

otherCount = purchase_data_df.loc[purchase_data_df["Gender"] == 'Other / Non-Disclosed', :]
otherPlayerCount = otherCount['SN'].value_counts().count()
remainingPercentage = otherPlayerCount/playerCount
print("Other / Non-Disclosed: "+ str(otherPlayerCount))
print("Percentage of Other/Non-Disclosed players: "+"{:.2%}".format(remainingPercentage))
```

    Other / Non-Disclosed: 8
    Percentage of Other/Non-Disclosed players: 1.40%



```python
# Gender Demographics DataFrame

raw_gender_data = {'Gender': ['Male', 'Female', 'Other / Non-Disclosed'],
            'Total Count': ['465', '100', '8'],
            'Percentage of Players': ['81.15', '17.45', '1.40']}

gender_demographics_df = pd.DataFrame(raw_gender_data)
gender_demographics_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing analysis by gender

groupByGender_df = purchase_data_df.groupby(['Gender'])

summaryTable_gender = pd.DataFrame({"Purchase Count": groupByGender_df["Gender"].count(),
                           "Avg Purchase Price": groupByGender_df["Price"].mean(),
                            "Total Purchase Value": groupByGender_df["Price"].sum()})
summaryTable_gender
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>$2.82</td>
      <td>136</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>$2.95</td>
      <td>633</td>
      <td>$1,867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>$3.25</td>
      <td>11</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Normalized totals equals "Total Purchase Value" / "Total Count of Players"

raw_norm_data = {'Gender': ['Female', 'Male', 'Other / Non-Disclosed'],
            'Normalized Totals': ['$3.83', '$4.02', '$4.47'],
                "Total Purchase Value": groupByGender_df["Price"].sum()}

norm_totals_gender_df = pd.DataFrame(raw_norm_data, columns=["Gender", "Normalized Totals", "Total Purchase Value"])
norm_totals_gender_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Normalized Totals</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>Female</td>
      <td>$3.83</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>Male</td>
      <td>$4.02</td>
      <td>$1,867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>Other / Non-Disclosed</td>
      <td>$4.47</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge two dataframes using a left join
gender_table = pd.merge(organized_summaryTable_gender, norm_totals_gender_df, on="Total Purchase Value", how="left")
gender_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Gender</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>Female</td>
      <td>$3.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>633</td>
      <td>$2.95</td>
      <td>$1,867.68</td>
      <td>Male</td>
      <td>$4.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>Other / Non-Disclosed</td>
      <td>$4.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
gender_table.columns
```




    Index(['Purchase Count', 'Avg Purchase Price', 'Total Purchase Value',
           'Gender', 'Normalized Totals'],
          dtype='object')




```python
# Reorganize columns
gender_table_organized = gender_table[["Gender","Purchase Count","Avg Purchase Price","Total Purchase Value", "Normalized Totals"]]
gender_table_organized.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$3.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>$2.95</td>
      <td>$1,867.68</td>
      <td>$4.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>$4.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchase count broken into a bin of 4 years
# Determine maximum age for bin.
max_age_Purchases = purchase_data_df['Age'].max()
max_age_Purchases

# Maximum age is 45.
```




    45




```python
# Determine minimum age for bin.
min_age_Purchases = purchase_data_df['Age'].min()
min_age_Purchases

# Minimum age is 7.

```




    7




```python
# Bins need to range from age 7 to age 45 and broken down into 4 year segments.

bins = [0, 9, 14, 19, 24, 29, 34, 39, max_age_Purchases]

# Create the names for the 10 bins
group_names = ['<10', '10-14', '15-19', '20-24','25-29', '30-34', '35-39', '40+']
```


```python
# Cut Purchase Count and place counts into bins

# totalPurchases 

purchase_count_series = pd.cut(purchase_data_df["Age"], bins, labels=group_names)
purchase_count_series.head(10)
```




    0    35-39
    1    20-24
    2    30-34
    3    20-24
    4    20-24
    5    20-24
    6    20-24
    7    25-29
    8    25-29
    9    30-34
    Name: Age, dtype: category
    Categories (8, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39 < 40+]




```python
# Determine the average purchase price per demographic.
# Create a new age demographic column to help visualize data.

purchase_data_df["Age Demographic"] = purchase_count_series
purchase_data_df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Demographic</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>$3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>$2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>$2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>$1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>$1.73</td>
      <td>Tanimnya91</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>$4.57</td>
      <td>Undjaskla97</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>$3.32</td>
      <td>Iathenudil29</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>$2.77</td>
      <td>Sondenasta63</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>31</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>$4.53</td>
      <td>Hilaerin92</td>
      <td>30-34</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Determine total counts of players in age bins.

under10Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '<10', :]
under10PlayerCount = under10Count['SN'].value_counts().count()

print(under10PlayerCount)
under10Percentage = under10PlayerCount/playerCount

print('{:.2%}'.format(under10Percentage))


```

    19
    3.32%



```python
age1014Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '10-14', :]
age1014PlayerCount = age1014Count['SN'].value_counts().count()

print(age1014PlayerCount)
age1014Percentage = age1014PlayerCount/playerCount

print('{:.2%}'.format(age1014Percentage))
```

    23
    4.01%



```python
age1519Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '15-19', :]
age1519PlayerCount = age1519Count['SN'].value_counts().count()

print(age1519PlayerCount)
age1519Percentage = age1519PlayerCount/playerCount

print('{:.2%}'.format(age1519Percentage))
```

    100
    17.45%



```python
age2024Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '20-24', :]
age2024PlayerCount = age2024Count['SN'].value_counts().count()

print(age2024PlayerCount)
age2024Percentage = age2024PlayerCount/playerCount

print('{:.2%}'.format(age2024Percentage))
```

    259
    45.20%



```python
age2529Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '25-29', :]
age2529PlayerCount = age2529Count['SN'].value_counts().count()

print(age2529PlayerCount)
age2529Percentage = age2529PlayerCount/playerCount

print('{:.2%}'.format(age2529Percentage))
```

    87
    15.18%



```python
age3034Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '30-34', :]
age3034PlayerCount = age3034Count['SN'].value_counts().count()

print(age3034PlayerCount)
age3034Percentage = age3034PlayerCount/playerCount

print('{:.2%}'.format(age3034Percentage))
```

    47
    8.20%



```python
age3539Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '35-39', :]
age3539PlayerCount = age3539Count['SN'].value_counts().count()

print(age3539PlayerCount)
age3539Percentage = age3539PlayerCount/playerCount

print('{:.2%}'.format(age3539Percentage))
```

    27
    4.71%



```python
over40Count = purchase_data_df.loc[purchase_data_df["Age Demographic"] == '40+', :]
over40PlayerCount = over40Count['SN'].value_counts().count()

print(over40PlayerCount)
over40Percentage = over40PlayerCount/playerCount

print('{:.2%}'.format(over40Percentage))
```

    11
    1.92%



```python
# Create age demographic DataFrame for visual purposes.

raw_age_data = {'Age Demographic': ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+'],
            'Total Count': ['19', '23', '100', '259', '87', '47', '27', '11'],
               'Percentage of Players': ['3.32','4.01','17.45','45.20', '15.18', '8.20','4.71','1.92']}

age_demographics_df = pd.DataFrame(raw_age_data, columns=["Age Demographic", "Total Count", "Percentage of Players"])
age_demographics_df.set_index("Age Demographic")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Demographic</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>19</td>
      <td>3.32</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>23</td>
      <td>4.01</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>45.20</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>15.18</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>8.20</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>4.71</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>11</td>
      <td>1.92</td>
    </tr>
  </tbody>
</table>
</div>




```python
# GroupBy analysis by Age Demographic.

groupByAge_df = purchase_data_df.groupby(['Age Demographic'])

summaryTable_age = pd.DataFrame({"Purchase Count": groupByAge_df["Age Demographic"].count(),
                           "Avg Purchase Price": groupByAge_df["Price"].mean(),
                            "Total Purchase Value": groupByAge_df["Price"].sum()})
summaryTable_age

# Reorganizing the columns
organized_summaryTable_age = summaryTable_age[["Purchase Count","Avg Purchase Price","Total Purchase Value"]]

organized_summaryTable_age
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Demographic</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>28</td>
      <td>$2.98</td>
      <td>$83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>35</td>
      <td>$2.77</td>
      <td>$96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>133</td>
      <td>$2.91</td>
      <td>$386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>336</td>
      <td>$2.91</td>
      <td>$978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>125</td>
      <td>$2.96</td>
      <td>$370.33</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>64</td>
      <td>$3.08</td>
      <td>$197.25</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>42</td>
      <td>$2.84</td>
      <td>$119.40</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>17</td>
      <td>$3.16</td>
      <td>$53.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Normalized totals equals "Total Purchase Value" / "Total Count of Players"

raw_norm_data_age = {'Age Demographic': ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+'],
            'Normalized Totals': ['$4.39', '$4.22', '$3.86', '$3.78', '$4.26', '$4.20', '$4.42', '$4.89'],
                "Total Purchase Value": groupByAge_df["Price"].sum()}

norm_totals_age_df = pd.DataFrame(raw_norm_data_age, columns=["Age Demographic", "Normalized Totals", "Total Purchase Value"])
norm_totals_age_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Demographic</th>
      <th>Normalized Totals</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Demographic</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>&lt;10</td>
      <td>$4.39</td>
      <td>$83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>10-14</td>
      <td>$4.22</td>
      <td>$96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>15-19</td>
      <td>$3.86</td>
      <td>$386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>20-24</td>
      <td>$3.78</td>
      <td>$978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>25-29</td>
      <td>$4.26</td>
      <td>$370.33</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>30-34</td>
      <td>$4.20</td>
      <td>$197.25</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>35-39</td>
      <td>$4.42</td>
      <td>$119.40</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>40+</td>
      <td>$4.89</td>
      <td>$53.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge two dataframes using a left join
age_table = pd.merge(organized_summaryTable_age, norm_totals_age_df, on="Total Purchase Value", how="left")
age_table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Age Demographic</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>28</td>
      <td>$2.98</td>
      <td>$83.46</td>
      <td>&lt;10</td>
      <td>$4.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>$2.77</td>
      <td>$96.95</td>
      <td>10-14</td>
      <td>$4.22</td>
    </tr>
    <tr>
      <th>2</th>
      <td>133</td>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>15-19</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>336</td>
      <td>$2.91</td>
      <td>$978.77</td>
      <td>20-24</td>
      <td>$3.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>125</td>
      <td>$2.96</td>
      <td>$370.33</td>
      <td>25-29</td>
      <td>$4.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>64</td>
      <td>$3.08</td>
      <td>$197.25</td>
      <td>30-34</td>
      <td>$4.20</td>
    </tr>
    <tr>
      <th>6</th>
      <td>42</td>
      <td>$2.84</td>
      <td>$119.40</td>
      <td>35-39</td>
      <td>$4.42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17</td>
      <td>$3.16</td>
      <td>$53.75</td>
      <td>40+</td>
      <td>$4.89</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reorganize columns
age_table_organized = age_table[["Age Demographic","Purchase Count","Avg Purchase Price","Total Purchase Value", "Normalized Totals"]]
age_table_organized
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Demographic</th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>28</td>
      <td>$2.98</td>
      <td>$83.46</td>
      <td>$4.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>35</td>
      <td>$2.77</td>
      <td>$96.95</td>
      <td>$4.22</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
      <td>$2.91</td>
      <td>$978.77</td>
      <td>$3.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
      <td>$2.96</td>
      <td>$370.33</td>
      <td>$4.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
      <td>$3.08</td>
      <td>$197.25</td>
      <td>$4.20</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
      <td>$2.84</td>
      <td>$119.40</td>
      <td>$4.42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40+</td>
      <td>17</td>
      <td>$3.16</td>
      <td>$53.75</td>
      <td>$4.89</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Move SN over to the left-most column for visual purposes.
spenders_df = purchase_data_df[['SN', 'Age', 'Gender', 'Item ID', 'Item Name', 'Price']]
spenders_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aelalis34</td>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>$3.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Eolo46</td>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>$2.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Assastnya25</td>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>$2.46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pheusrical25</td>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$1.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>$1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sorting price by SN.
top_spenders_groups = spenders_df.sort_values("Price", ascending=False)
top_spenders_groups.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>83</th>
      <td>Frichaststa61</td>
      <td>25</td>
      <td>Female</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>$4.95</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Saistyphos30</td>
      <td>32</td>
      <td>Female</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>$4.95</td>
    </tr>
    <tr>
      <th>657</th>
      <td>Tyarithn67</td>
      <td>28</td>
      <td>Male</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>$4.95</td>
    </tr>
    <tr>
      <th>388</th>
      <td>Palurrian69</td>
      <td>15</td>
      <td>Male</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>$4.95</td>
    </tr>
    <tr>
      <th>227</th>
      <td>Qiluard68</td>
      <td>20</td>
      <td>Male</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>$4.95</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Experimenting with groupby function.
top_spenders_groupby = spenders_df.groupby("Price")
top_spenders_groupby.max().head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
    </tr>
    <tr>
      <th>Price</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>$1.03</th>
      <td>Tyaelo67</td>
      <td>37</td>
      <td>Male</td>
      <td>95</td>
      <td>Soul Infused Crystal</td>
    </tr>
    <tr>
      <th>$1.06</th>
      <td>Tillyrin30</td>
      <td>30</td>
      <td>Male</td>
      <td>74</td>
      <td>Yearning Crusher</td>
    </tr>
    <tr>
      <th>$1.11</th>
      <td>Zhisrisu83</td>
      <td>20</td>
      <td>Male</td>
      <td>82</td>
      <td>Nirvana</td>
    </tr>
    <tr>
      <th>$1.14</th>
      <td>Sundista85</td>
      <td>25</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
    </tr>
    <tr>
      <th>$1.16</th>
      <td>Undirrasta74</td>
      <td>30</td>
      <td>Male</td>
      <td>156</td>
      <td>Soul-Forged Steel Shortsword</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group by SN
groupBySN_df = purchase_data_df.groupby(['SN'])

summaryTable_SN = pd.DataFrame({"Total Purchase Value": groupBySN_df["Price"].sum(),
                                "Purchase Count": groupBySN_df["SN"].count(),
                               "Avg Purchase Price": groupBySN_df["Price"].mean()})
summaryTable_SN.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>$2.46</td>
      <td>1</td>
      <td>$2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>$2.23</td>
      <td>3</td>
      <td>$6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>$1.93</td>
      <td>3</td>
      <td>$5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>$2.46</td>
      <td>1</td>
      <td>$2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>$1.27</td>
      <td>1</td>
      <td>$1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Determine top spenders.

Top_5_df = summaryTable_SN.sort_values("Total Purchase Value", ascending=False)

# Reorganize columns
Top_5_df_org = Top_5_df[["Purchase Count", "Avg Purchase Price", "Total Purchase Value"]]
Top_5_df_org.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Avg Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Identify the 5 most popular items by purchase count
# Group by Item ID

groupByItem_df = purchase_data_df.groupby(['Item ID'])

summaryTable_Item = pd.DataFrame({"Purchase Count": groupByItem_df["Item Name"].count(),
                                 "Item Name": groupByItem_df["Item Name"].unique(),
                                 "Item Price": groupByItem_df["Price"].unique(),
                                 "Total Purchase Value": groupByItem_df["Price"].sum()})
summaryTable_Item.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>[Splinter]</td>
      <td>[1.82]</td>
      <td>1</td>
      <td>$1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>[Crucifer]</td>
      <td>[2.2800000000000002]</td>
      <td>4</td>
      <td>$9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>[Verdict]</td>
      <td>[3.4]</td>
      <td>1</td>
      <td>$3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>[Phantomlight]</td>
      <td>[1.79]</td>
      <td>1</td>
      <td>$1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>[Bloodlord's Fetish]</td>
      <td>[2.2800000000000002]</td>
      <td>1</td>
      <td>$2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sort to find the top 5 most popular items by purchase count
Top_5_item = summaryTable_Item.sort_values("Purchase Count", ascending=False)
Top_5_item.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>[Betrayal, Whisper of Grieving Widows]</td>
      <td>[2.35]</td>
      <td>11</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>[Arcane Gem]</td>
      <td>[2.23]</td>
      <td>11</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <td>[Trickster]</td>
      <td>[2.07]</td>
      <td>9</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <td>[Woeful Adamantite Claymore]</td>
      <td>[1.24]</td>
      <td>9</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>[Serenity]</td>
      <td>[1.49]</td>
      <td>9</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Identify the 5 most profitable items by total purchase value
Top_5_item_value = summaryTable_Item.sort_values("Total Purchase Value", ascending=False)
Top_5_item_value.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>[Retribution Axe]</td>
      <td>[4.14]</td>
      <td>9</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>[Spectral Diamond Doomblade]</td>
      <td>[4.25]</td>
      <td>7</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>[Orenmir]</td>
      <td>[4.95]</td>
      <td>6</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>[Singed Scalpel]</td>
      <td>[4.87]</td>
      <td>6</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>[Splitter, Foe Of Subtlety]</td>
      <td>[3.61]</td>
      <td>8</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


