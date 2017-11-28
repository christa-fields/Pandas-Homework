

```python
# Dependencies
import pandas as pd
import json
```


```python
# load JSON
purchase_data_1 ="HeroesOfPymoli/purchase_data.json"
purchase_data_2 ="HeroesOfPymoli/purchase_data2.json"
```


```python
# Read with pandas
purchase_data_2_pd = pd.read_json(purchase_data_2)
purchase_data_2_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_players= purchase_data_2_pd.drop_duplicates(subset=["SN","Age","Gender"],keep="last")
len(total_players)
```




    74




```python
#Number of Unique Items
unique_items =list(purchase_data_2_pd['Item Name'].unique())
number_unique_items= len(unique_items)
number_unique_items
```




    63




```python
#Average Purchase Price
average_price =purchase_data_2_pd["Price"].mean()
average_price
```




    2.9243589743589733




```python
#Total Number of Purchases

count_purchases= purchase_data_2_pd["Price"].value_counts()
total_purchases = len(count_purchases)
total_purchases
```




    60




```python
#Total Revenue
total_revenue = purchase_data_2_pd["Price"].sum()
total_revenue
```




    228.0999999999999




```python
#Purchasing Analysis (Total)


purchasing_analysis_total = [{"Number of Unique Items":"63","Average Price":"$2.92","Number of Purchases":"60", "Total Revenue":"$228.09"}]

df_purchasing_analysis_total = pd.DataFrame(purchasing_analysis_total)
df_purchasing_analysis_total

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Number of Unique Items</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.92</td>
      <td>60</td>
      <td>63</td>
      <td>$228.09</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Group by gender

gender_groups_df = purchase_data_2_pd.groupby("Gender")
gender_groups_df.max()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>39</td>
      <td>173</td>
      <td>Verdict</td>
      <td>4.71</td>
      <td>Undosian34</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>40</td>
      <td>181</td>
      <td>Wolf</td>
      <td>4.81</td>
      <td>Zhisrisu83</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>12</td>
      <td>176</td>
      <td>Relentless Iron Skewer</td>
      <td>2.12</td>
      <td>Inadeu25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Find the total number of gender

gender_count = pd.DataFrame(gender_groups_df["Gender"].count())
gender_count
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>13</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>64</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Find the sum of Gender column

#total_count =  pd.DataFrame(gender_groups_df["Gender"].sum())
#total_count

#total_count =gender['Gender'].sum()
#total_count

```


```python
#Find percentage of Players by Gender

#percentage_by_gender =  pd.DataFrame(gender_groups_df["Gender"]/78)
#percentage_by_gender
```


```python
#Purchase Count

purchase_count = pd.DataFrame(gender_groups_df["Item ID"].count())
purchase_count
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>13</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>64</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Average Purchase Price
average_purchase_price = pd.DataFrame(gender_groups_df["Price"].mean())
average_purchase_price
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>3.183077</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.884375</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>2.120000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Purchase Value
total_purchase_value = pd.DataFrame(gender_groups_df["Price"].sum())
total_purchase_value
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>41.38</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>184.60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>2.12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Normalized Totals
normalized_totals = pd.DataFrame(gender_groups_df["Price"].mean())
normalized_totals
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>3.183077</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.884375</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>2.120000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis by Gender
```


```python
# Create the bins in which Data will be held
# Bins are  <10, 10-14, 15-19, etc.
bins = [10, 14, 19, 24, 29, 34, 39,100]
```


```python
#Create labels
age_group_names = ['<10', '10-14', '15-19', '20-24', '25-29','30-34','35-39']
```


```python
#Cut Age into categories
categories = pd.cut(purchase_data_2_pd['Age'], bins, labels=age_group_names)
purchase_data_2_pd['categories'] = pd.cut(purchase_data_2_pd['Age'], bins, labels=age_group_names)
categories
```




    0     15-19
    1     15-19
    2     10-14
    3     10-14
    4     15-19
    5       NaN
    6     35-39
    7     20-24
    8     10-14
    9     30-34
    10    15-19
    11    30-34
    12    15-19
    13    25-29
    14      NaN
    15    15-19
    16    15-19
    17      NaN
    18      <10
    19    15-19
    20    30-34
    21      <10
    22    10-14
    23    15-19
    24    15-19
    25    10-14
    26      NaN
    27    20-24
    28    15-19
    29    15-19
          ...  
    48    20-24
    49    15-19
    50    15-19
    51    20-24
    52    15-19
    53    10-14
    54    20-24
    55    15-19
    56    10-14
    57    15-19
    58    25-29
    59    30-34
    60    15-19
    61    15-19
    62    10-14
    63      <10
    64    15-19
    65    15-19
    66    15-19
    67    15-19
    68    15-19
    69    25-29
    70    20-24
    71    20-24
    72    15-19
    73    30-34
    74    30-34
    75    10-14
    76    15-19
    77    15-19
    Name: Age, Length: 78, dtype: category
    Categories (7, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39]




```python
#Purchase Count
purchase_count= pd.value_counts(purchase_data_2_pd['categories'])
purchase_count
```




    15-19    36
    10-14    11
    20-24     9
    25-29     7
    30-34     6
    <10       3
    35-39     1
    Name: categories, dtype: int64




```python
#Average Purchase Price

average_purchase_price =age_groups_df['Price'].mean(), bins
average_purchase_price

```




    (categories
     <10      2.986667
     10-14    2.764545
     15-19    3.024722
     20-24    2.901111
     25-29    1.984286
     30-34    3.561667
     35-39    4.650000
     Name: Price, dtype: float64, [10, 14, 19, 24, 29, 34, 39, 100])




```python
#Total Purchase Value
total_purchase_value = age_groups_df["Price"].sum(), bins
total_purchase_value
```




    (categories
     <10        8.96
     10-14     30.41
     15-19    108.89
     20-24     26.11
     25-29     13.89
     30-34     21.37
     35-39      4.65
     Name: Price, dtype: float64, [10, 14, 19, 24, 29, 34, 39, 100])




```python
#Normalized Totals
normalized_totals = age_groups_df["Price"].mean(), bins
normalized_totals
```




    (categories
     <10      2.986667
     10-14    2.764545
     15-19    3.024722
     20-24    2.901111
     25-29    1.984286
     30-34    3.561667
     35-39    4.650000
     Name: Price, dtype: float64, [10, 14, 19, 24, 29, 34, 39, 100])




```python
#Age Demographics: broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)

#purchase_data_2_pd['Average Purchase Price'] = pd.cut(purchase_data_2_pd['Age'], bins, labels=age_group_names)
#purchase_data_2_pd

#age_groups_df = purchase_data_2_pd.groupby("categories")
#age_groups_df.max()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th>categories</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>12</td>
      <td>Other / Non-Disclosed</td>
      <td>176</td>
      <td>Relentless Iron Skewer</td>
      <td>3.85</td>
      <td>Isristira52</td>
      <td>&lt;10</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>18</td>
      <td>Male</td>
      <td>180</td>
      <td>Twilight's Carver</td>
      <td>4.78</td>
      <td>Yarmol79</td>
      <td>10-14</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>24</td>
      <td>Male</td>
      <td>181</td>
      <td>War-Forged Gold Deflector</td>
      <td>4.71</td>
      <td>Zhisrisu83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>28</td>
      <td>Male</td>
      <td>127</td>
      <td>Wolf</td>
      <td>4.81</td>
      <td>Undirra90</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>34</td>
      <td>Male</td>
      <td>138</td>
      <td>Wolf</td>
      <td>2.88</td>
      <td>Undosian34</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>39</td>
      <td>Male</td>
      <td>173</td>
      <td>Verdict</td>
      <td>4.49</td>
      <td>Streural92</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>40</td>
      <td>Male</td>
      <td>148</td>
      <td>Warmonger, Gift of Suffering's End</td>
      <td>4.65</td>
      <td>Aerithllora36</td>
      <td>35-39</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders
#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
```


```python
#Purchase Count

#purchase_counts= pd.DataFrame(purchase_data_2_pd["Item ID"].value_counts())
#purchase_counts

purchase_data_2_pd["Total Purchase Counts"]= pd.DataFrame(purchase_data_2_pd["Item ID"].value_counts())
purchase_data_2_pd.head(5)

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>categories</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Counts</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>15-19</td>
      <td>15-19</td>
      <td>1.0</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>15-19</td>
      <td>15-19</td>
      <td>1.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>10-14</td>
      <td>10-14</td>
      <td>1.0</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>10-14</td>
      <td>10-14</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>15-19</td>
      <td>15-19</td>
      <td>1.0</td>
      <td>4.11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Average Purchase Price
purchase_data_2_pd["Average Purchase Price"]= pd.DataFrame(purchase_data_2_pd["Price"])
purchase_data_2_pd.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>categories</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Counts</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>15-19</td>
      <td>4.49</td>
      <td>1.0</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>15-19</td>
      <td>3.36</td>
      <td>1.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>10-14</td>
      <td>2.63</td>
      <td>1.0</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>10-14</td>
      <td>2.55</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>15-19</td>
      <td>4.11</td>
      <td>1.0</td>
      <td>4.11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Purchase Value

purchase_data_2_pd["Total Purchase Value"]= pd.DataFrame(purchase_data_2_pd["Price"] * purchase_data_2_pd["Item ID"].value_counts())
purchase_data_2_pd.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>categories</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Counts</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>15-19</td>
      <td>15-19</td>
      <td>1.0</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>15-19</td>
      <td>15-19</td>
      <td>1.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>10-14</td>
      <td>10-14</td>
      <td>1.0</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>10-14</td>
      <td>10-14</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>15-19</td>
      <td>15-19</td>
      <td>1.0</td>
      <td>4.11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#SN

SN_groups_df = purchase_data_2_pd.groupby("SN")
SN_groups_df.max()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>categories</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Counts</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>Splitter, Foe Of Subtlety</td>
      <td>4.15</td>
      <td>15-19</td>
      <td>4.15</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>40</td>
      <td>Male</td>
      <td>148</td>
      <td>Warmonger, Gift of Suffering's End</td>
      <td>4.65</td>
      <td>35-39</td>
      <td>4.65</td>
      <td>1.0</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <td>39</td>
      <td>Female</td>
      <td>2</td>
      <td>Verdict</td>
      <td>2.65</td>
      <td>30-34</td>
      <td>2.65</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <td>36</td>
      <td>Male</td>
      <td>139</td>
      <td>Mercy, Katana of Dismay</td>
      <td>4.25</td>
      <td>30-34</td>
      <td>4.25</td>
      <td>1.0</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>21</td>
      <td>Male</td>
      <td>82</td>
      <td>Nirvana</td>
      <td>3.36</td>
      <td>15-19</td>
      <td>3.36</td>
      <td>1.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>Aiduecal76</th>
      <td>8</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>1.42</td>
      <td>NaN</td>
      <td>1.42</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Airi27</th>
      <td>24</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>1.91</td>
      <td>15-19</td>
      <td>1.91</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Airithrin43</th>
      <td>21</td>
      <td>Female</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>2.26</td>
      <td>15-19</td>
      <td>2.26</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Alarap40</th>
      <td>24</td>
      <td>Female</td>
      <td>117</td>
      <td>Heartstriker, Legacy of the Light</td>
      <td>4.71</td>
      <td>15-19</td>
      <td>4.71</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Ardcil81</th>
      <td>38</td>
      <td>Male</td>
      <td>163</td>
      <td>Thunderfury Scimitar</td>
      <td>4.16</td>
      <td>30-34</td>
      <td>4.16</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Arithllorin55</th>
      <td>21</td>
      <td>Male</td>
      <td>90</td>
      <td>Betrayer</td>
      <td>4.12</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Assistast50</th>
      <td>23</td>
      <td>Female</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.95</td>
      <td>15-19</td>
      <td>2.95</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chamalo71</th>
      <td>34</td>
      <td>Male</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>1.08</td>
      <td>25-29</td>
      <td>1.08</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chamast86</th>
      <td>35</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>30-34</td>
      <td>4.49</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chamjaskya75</th>
      <td>17</td>
      <td>Male</td>
      <td>180</td>
      <td>Stormcaller</td>
      <td>2.77</td>
      <td>10-14</td>
      <td>2.77</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chaniman66</th>
      <td>24</td>
      <td>Male</td>
      <td>164</td>
      <td>Swan Song, Gouger Of Terror</td>
      <td>1.92</td>
      <td>15-19</td>
      <td>1.92</td>
      <td>2.0</td>
      <td>2.62</td>
    </tr>
    <tr>
      <th>Chanirra64</th>
      <td>18</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>4.78</td>
      <td>10-14</td>
      <td>4.78</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chanjasksda31</th>
      <td>33</td>
      <td>Male</td>
      <td>17</td>
      <td>Lazarus, Terror of the Earth</td>
      <td>1.96</td>
      <td>25-29</td>
      <td>1.96</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chrathybust28</th>
      <td>21</td>
      <td>Male</td>
      <td>16</td>
      <td>Restored Bauble</td>
      <td>2.15</td>
      <td>15-19</td>
      <td>2.15</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Eolideu96</th>
      <td>18</td>
      <td>Male</td>
      <td>111</td>
      <td>Misery's End</td>
      <td>1.79</td>
      <td>10-14</td>
      <td>1.79</td>
      <td>1.0</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>Eollym91</th>
      <td>20</td>
      <td>Male</td>
      <td>18</td>
      <td>Torchlight, Bond of Storms</td>
      <td>3.75</td>
      <td>15-19</td>
      <td>3.75</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Eoralphos86</th>
      <td>11</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>2.99</td>
      <td>&lt;10</td>
      <td>2.99</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Ethralan59</th>
      <td>33</td>
      <td>Male</td>
      <td>129</td>
      <td>Fate, Vengeance of Eternal Justice</td>
      <td>2.88</td>
      <td>25-29</td>
      <td>2.88</td>
      <td>1.0</td>
      <td>2.88</td>
    </tr>
    <tr>
      <th>Eusty71</th>
      <td>25</td>
      <td>Male</td>
      <td>84</td>
      <td>Arcane Gem</td>
      <td>4.81</td>
      <td>20-24</td>
      <td>4.81</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Eustyria89</th>
      <td>30</td>
      <td>Male</td>
      <td>60</td>
      <td>Wolf</td>
      <td>2.70</td>
      <td>25-29</td>
      <td>2.70</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Filon68</th>
      <td>23</td>
      <td>Male</td>
      <td>176</td>
      <td>Relentless Iron Skewer</td>
      <td>2.12</td>
      <td>15-19</td>
      <td>2.12</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Firon67</th>
      <td>23</td>
      <td>Female</td>
      <td>68</td>
      <td>Storm-Weaver, Slayer of Inception</td>
      <td>4.39</td>
      <td>15-19</td>
      <td>4.39</td>
      <td>2.0</td>
      <td>8.78</td>
    </tr>
    <tr>
      <th>Frichilsa31</th>
      <td>20</td>
      <td>Male</td>
      <td>14</td>
      <td>Possessed Core</td>
      <td>2.82</td>
      <td>15-19</td>
      <td>2.82</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Haerithp41</th>
      <td>23</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>15-19</td>
      <td>4.11</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hainaria90</th>
      <td>8</td>
      <td>Male</td>
      <td>8</td>
      <td>Purgatory, Gem of Regret</td>
      <td>2.22</td>
      <td>NaN</td>
      <td>2.22</td>
      <td>1.0</td>
      <td>2.22</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Jiskimsda56</th>
      <td>24</td>
      <td>Male</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>1.08</td>
      <td>15-19</td>
      <td>1.08</td>
      <td>1.0</td>
      <td>1.08</td>
    </tr>
    <tr>
      <th>Jiskjask76</th>
      <td>21</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>4.59</td>
      <td>15-19</td>
      <td>4.59</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Lassimla92</th>
      <td>20</td>
      <td>Male</td>
      <td>158</td>
      <td>Darkheart, Butcher of the Champion</td>
      <td>1.94</td>
      <td>15-19</td>
      <td>1.94</td>
      <td>1.0</td>
      <td>1.94</td>
    </tr>
    <tr>
      <th>Lirtassa77</th>
      <td>20</td>
      <td>Female</td>
      <td>90</td>
      <td>Betrayer</td>
      <td>4.12</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>1.0</td>
      <td>4.12</td>
    </tr>
    <tr>
      <th>Lirtastan49</th>
      <td>25</td>
      <td>Male</td>
      <td>127</td>
      <td>Heartseeker, Reaver of Souls</td>
      <td>1.34</td>
      <td>20-24</td>
      <td>1.34</td>
      <td>1.0</td>
      <td>1.34</td>
    </tr>
    <tr>
      <th>Lirtistanya48</th>
      <td>7</td>
      <td>Male</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>1.29</td>
      <td>NaN</td>
      <td>1.29</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Lisirra44</th>
      <td>21</td>
      <td>Male</td>
      <td>180</td>
      <td>Stormcaller</td>
      <td>2.77</td>
      <td>15-19</td>
      <td>2.77</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Lisosiast26</th>
      <td>24</td>
      <td>Male</td>
      <td>6</td>
      <td>Rusty Skull</td>
      <td>3.58</td>
      <td>15-19</td>
      <td>3.58</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Palyon91</th>
      <td>28</td>
      <td>Male</td>
      <td>1</td>
      <td>Crucifer</td>
      <td>3.67</td>
      <td>20-24</td>
      <td>3.67</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Pharithdil38</th>
      <td>16</td>
      <td>Female</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.89</td>
      <td>10-14</td>
      <td>1.89</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Pheodaisun84</th>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>2.26</td>
      <td>15-19</td>
      <td>2.26</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Philodil43</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>15-19</td>
      <td>4.11</td>
      <td>1.0</td>
      <td>4.11</td>
    </tr>
    <tr>
      <th>Rarallo90</th>
      <td>9</td>
      <td>Male</td>
      <td>156</td>
      <td>Soul-Forged Steel Shortsword</td>
      <td>4.53</td>
      <td>NaN</td>
      <td>4.53</td>
      <td>1.0</td>
      <td>4.53</td>
    </tr>
    <tr>
      <th>Saralp86</th>
      <td>25</td>
      <td>Male</td>
      <td>64</td>
      <td>Fusion Pummel</td>
      <td>2.42</td>
      <td>20-24</td>
      <td>2.42</td>
      <td>1.0</td>
      <td>2.42</td>
    </tr>
    <tr>
      <th>Seostylis96</th>
      <td>16</td>
      <td>Female</td>
      <td>94</td>
      <td>Mourning Blade</td>
      <td>3.64</td>
      <td>10-14</td>
      <td>3.64</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Shaidanu32</th>
      <td>16</td>
      <td>Male</td>
      <td>172</td>
      <td>Blade of the Grave</td>
      <td>2.71</td>
      <td>10-14</td>
      <td>2.71</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sondassasya91</th>
      <td>20</td>
      <td>Female</td>
      <td>170</td>
      <td>Shadowsteel</td>
      <td>1.74</td>
      <td>15-19</td>
      <td>1.74</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sondim43</th>
      <td>23</td>
      <td>Male</td>
      <td>94</td>
      <td>Mourning Blade</td>
      <td>3.64</td>
      <td>15-19</td>
      <td>3.64</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Streural92</th>
      <td>35</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.81</td>
      <td>30-34</td>
      <td>1.81</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sundaky74</th>
      <td>25</td>
      <td>Male</td>
      <td>117</td>
      <td>Wolf</td>
      <td>4.71</td>
      <td>20-24</td>
      <td>4.71</td>
      <td>1.0</td>
      <td>4.71</td>
    </tr>
    <tr>
      <th>Syalallodil59</th>
      <td>20</td>
      <td>Male</td>
      <td>134</td>
      <td>Undead Crusader</td>
      <td>2.15</td>
      <td>15-19</td>
      <td>2.15</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Undadar97</th>
      <td>25</td>
      <td>Male</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>1.29</td>
      <td>20-24</td>
      <td>1.29</td>
      <td>1.0</td>
      <td>1.29</td>
    </tr>
    <tr>
      <th>Undilsan50</th>
      <td>22</td>
      <td>Male</td>
      <td>94</td>
      <td>Mourning Blade</td>
      <td>3.64</td>
      <td>15-19</td>
      <td>3.64</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Undirra90</th>
      <td>28</td>
      <td>Male</td>
      <td>27</td>
      <td>Riddle, Tribute of Ended Dreams</td>
      <td>3.38</td>
      <td>20-24</td>
      <td>3.38</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Undirrasta74</th>
      <td>20</td>
      <td>Male</td>
      <td>64</td>
      <td>Fusion Pummel</td>
      <td>2.42</td>
      <td>15-19</td>
      <td>2.42</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Undosian34</th>
      <td>30</td>
      <td>Female</td>
      <td>105</td>
      <td>Hailstorm Shadowsteel Scythe</td>
      <td>1.02</td>
      <td>25-29</td>
      <td>1.02</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Yarith71</th>
      <td>8</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>4.36</td>
      <td>NaN</td>
      <td>4.36</td>
      <td>1.0</td>
      <td>4.36</td>
    </tr>
    <tr>
      <th>Yarithrgue83</th>
      <td>23</td>
      <td>Male</td>
      <td>181</td>
      <td>Reaper's Toll</td>
      <td>4.12</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>17</td>
      <td>Male</td>
      <td>79</td>
      <td>Alpha, Oath of Zeal</td>
      <td>1.31</td>
      <td>10-14</td>
      <td>1.31</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>24</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>1.36</td>
      <td>15-19</td>
      <td>1.36</td>
      <td>1.0</td>
      <td>1.36</td>
    </tr>
  </tbody>
</table>
<p>74 rows × 9 columns</p>
</div>




```python
#Most Popular Items
#Identify the 5 most popular items by purchase count, then list (in a table):
Item_groups_df = purchase_data_2_pd.groupby("Item Name")
Item_groups_df.max()

#Item_groups_dif.sort_values([Total Purchase Value])
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>SN</th>
      <th>categories</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Counts</th>
      <th>Total Purchase Value</th>
      <th>Purchase Counts_by_Item Name</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alpha, Oath of Zeal</th>
      <td>17</td>
      <td>Male</td>
      <td>79</td>
      <td>1.31</td>
      <td>Yarmol79</td>
      <td>10-14</td>
      <td>1.31</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Apocalyptic Battlescythe</th>
      <td>35</td>
      <td>Male</td>
      <td>93</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>30-34</td>
      <td>4.49</td>
      <td>1.0</td>
      <td>4.49</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Arcane Gem</th>
      <td>25</td>
      <td>Male</td>
      <td>84</td>
      <td>4.81</td>
      <td>Eusty71</td>
      <td>20-24</td>
      <td>4.81</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Betrayer</th>
      <td>21</td>
      <td>Male</td>
      <td>90</td>
      <td>4.12</td>
      <td>Lirtassa77</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>1.0</td>
      <td>4.12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Blade of the Grave</th>
      <td>16</td>
      <td>Male</td>
      <td>172</td>
      <td>2.71</td>
      <td>Shaidanu32</td>
      <td>10-14</td>
      <td>2.71</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Bloodlord's Fetish</th>
      <td>24</td>
      <td>Male</td>
      <td>4</td>
      <td>1.91</td>
      <td>Airi27</td>
      <td>15-19</td>
      <td>1.91</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Bonecarvin Battle Axe</th>
      <td>8</td>
      <td>Male</td>
      <td>44</td>
      <td>4.36</td>
      <td>Yarith71</td>
      <td>NaN</td>
      <td>4.36</td>
      <td>1.0</td>
      <td>4.36</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Celeste</th>
      <td>23</td>
      <td>Male</td>
      <td>91</td>
      <td>2.92</td>
      <td>Iskossaya95</td>
      <td>15-19</td>
      <td>2.92</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Crucifer</th>
      <td>32</td>
      <td>Male</td>
      <td>23</td>
      <td>3.67</td>
      <td>Palyon91</td>
      <td>25-29</td>
      <td>3.67</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Darkheart, Butcher of the Champion</th>
      <td>20</td>
      <td>Male</td>
      <td>158</td>
      <td>1.94</td>
      <td>Lassimla92</td>
      <td>15-19</td>
      <td>1.94</td>
      <td>1.0</td>
      <td>1.94</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Dawne</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>15-19</td>
      <td>3.36</td>
      <td>1.0</td>
      <td>3.36</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Deadline, Voice Of Subtlety</th>
      <td>25</td>
      <td>Male</td>
      <td>98</td>
      <td>1.29</td>
      <td>Undadar97</td>
      <td>20-24</td>
      <td>1.29</td>
      <td>1.0</td>
      <td>1.29</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Demise</th>
      <td>17</td>
      <td>Male</td>
      <td>71</td>
      <td>3.09</td>
      <td>Ilara98</td>
      <td>10-14</td>
      <td>3.09</td>
      <td>1.0</td>
      <td>3.09</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Exiled Doomblade</th>
      <td>24</td>
      <td>Male</td>
      <td>164</td>
      <td>1.31</td>
      <td>Chaniman66</td>
      <td>15-19</td>
      <td>1.31</td>
      <td>2.0</td>
      <td>2.62</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Exiled Mithril Longsword</th>
      <td>34</td>
      <td>Male</td>
      <td>126</td>
      <td>1.08</td>
      <td>Jiskimsda56</td>
      <td>25-29</td>
      <td>1.08</td>
      <td>1.0</td>
      <td>1.08</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>21</td>
      <td>Male</td>
      <td>108</td>
      <td>2.26</td>
      <td>Pheodaisun84</td>
      <td>15-19</td>
      <td>2.26</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fate, Vengeance of Eternal Justice</th>
      <td>33</td>
      <td>Male</td>
      <td>129</td>
      <td>2.88</td>
      <td>Ethralan59</td>
      <td>25-29</td>
      <td>2.88</td>
      <td>1.0</td>
      <td>2.88</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Feral Katana</th>
      <td>23</td>
      <td>Male</td>
      <td>154</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>15-19</td>
      <td>4.11</td>
      <td>1.0</td>
      <td>4.11</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fury</th>
      <td>11</td>
      <td>Male</td>
      <td>131</td>
      <td>2.99</td>
      <td>Eoralphos86</td>
      <td>&lt;10</td>
      <td>2.99</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fusion Pummel</th>
      <td>25</td>
      <td>Male</td>
      <td>64</td>
      <td>2.42</td>
      <td>Undirrasta74</td>
      <td>20-24</td>
      <td>2.42</td>
      <td>1.0</td>
      <td>2.42</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Ghost Reaver, Longsword of Magic</th>
      <td>23</td>
      <td>Female</td>
      <td>118</td>
      <td>2.95</td>
      <td>Assistast50</td>
      <td>15-19</td>
      <td>2.95</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Gladiator's Glaive</th>
      <td>20</td>
      <td>Male</td>
      <td>104</td>
      <td>1.84</td>
      <td>Ila44</td>
      <td>15-19</td>
      <td>1.84</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hailstorm Shadowsteel Scythe</th>
      <td>30</td>
      <td>Female</td>
      <td>105</td>
      <td>1.02</td>
      <td>Undosian34</td>
      <td>25-29</td>
      <td>1.02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Heartseeker, Reaver of Souls</th>
      <td>25</td>
      <td>Male</td>
      <td>127</td>
      <td>1.34</td>
      <td>Lirtastan49</td>
      <td>20-24</td>
      <td>1.34</td>
      <td>1.0</td>
      <td>1.34</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Heartstriker, Legacy of the Light</th>
      <td>25</td>
      <td>Male</td>
      <td>117</td>
      <td>4.71</td>
      <td>Sundaky74</td>
      <td>20-24</td>
      <td>4.71</td>
      <td>1.0</td>
      <td>4.71</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hero Cane</th>
      <td>18</td>
      <td>Male</td>
      <td>25</td>
      <td>4.78</td>
      <td>Chanirra64</td>
      <td>10-14</td>
      <td>4.78</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hope's End</th>
      <td>23</td>
      <td>Male</td>
      <td>70</td>
      <td>4.28</td>
      <td>Heosurnuru52</td>
      <td>15-19</td>
      <td>4.28</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Lazarus, Terror of the Earth</th>
      <td>33</td>
      <td>Male</td>
      <td>17</td>
      <td>1.96</td>
      <td>Chanjasksda31</td>
      <td>25-29</td>
      <td>1.96</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Malice, Legacy of the Queen</th>
      <td>15</td>
      <td>Male</td>
      <td>167</td>
      <td>3.25</td>
      <td>Heudai45</td>
      <td>10-14</td>
      <td>3.25</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mercy, Katana of Dismay</th>
      <td>36</td>
      <td>Male</td>
      <td>139</td>
      <td>4.25</td>
      <td>Aesurstilis64</td>
      <td>30-34</td>
      <td>4.25</td>
      <td>1.0</td>
      <td>4.25</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Orbit</th>
      <td>11</td>
      <td>Female</td>
      <td>41</td>
      <td>3.85</td>
      <td>Isristira52</td>
      <td>&lt;10</td>
      <td>3.85</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Peacekeeper, Wit of Dark Magic</th>
      <td>32</td>
      <td>Male</td>
      <td>138</td>
      <td>2.63</td>
      <td>Hairith93</td>
      <td>25-29</td>
      <td>2.63</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Possessed Core</th>
      <td>20</td>
      <td>Male</td>
      <td>14</td>
      <td>2.82</td>
      <td>Frichilsa31</td>
      <td>15-19</td>
      <td>2.82</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Primitive Blade</th>
      <td>24</td>
      <td>Male</td>
      <td>174</td>
      <td>1.36</td>
      <td>Zhisrisu83</td>
      <td>15-19</td>
      <td>1.36</td>
      <td>1.0</td>
      <td>1.36</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Purgatory, Gem of Regret</th>
      <td>8</td>
      <td>Male</td>
      <td>8</td>
      <td>2.22</td>
      <td>Hainaria90</td>
      <td>NaN</td>
      <td>2.22</td>
      <td>1.0</td>
      <td>2.22</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Putrid Fan</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>10-14</td>
      <td>2.63</td>
      <td>1.0</td>
      <td>2.63</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Reaper's Toll</th>
      <td>23</td>
      <td>Male</td>
      <td>181</td>
      <td>4.12</td>
      <td>Yarithrgue83</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Relentless Iron Skewer</th>
      <td>23</td>
      <td>Other / Non-Disclosed</td>
      <td>176</td>
      <td>2.12</td>
      <td>Inadeu25</td>
      <td>15-19</td>
      <td>2.12</td>
      <td>1.0</td>
      <td>2.12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Restored Bauble</th>
      <td>21</td>
      <td>Male</td>
      <td>16</td>
      <td>2.15</td>
      <td>Chrathybust28</td>
      <td>15-19</td>
      <td>2.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Riddle, Tribute of Ended Dreams</th>
      <td>28</td>
      <td>Male</td>
      <td>27</td>
      <td>3.38</td>
      <td>Undirra90</td>
      <td>20-24</td>
      <td>3.38</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Rusty Skull</th>
      <td>24</td>
      <td>Male</td>
      <td>6</td>
      <td>3.58</td>
      <td>Lisosiast26</td>
      <td>15-19</td>
      <td>3.58</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Shadowsteel</th>
      <td>20</td>
      <td>Female</td>
      <td>170</td>
      <td>1.74</td>
      <td>Sondassasya91</td>
      <td>15-19</td>
      <td>1.74</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sleepwalker</th>
      <td>35</td>
      <td>Male</td>
      <td>10</td>
      <td>1.81</td>
      <td>Streural92</td>
      <td>30-34</td>
      <td>1.81</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Soul-Forged Steel Shortsword</th>
      <td>9</td>
      <td>Male</td>
      <td>156</td>
      <td>4.53</td>
      <td>Rarallo90</td>
      <td>NaN</td>
      <td>4.53</td>
      <td>1.0</td>
      <td>4.53</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Splinter</th>
      <td>16</td>
      <td>Female</td>
      <td>0</td>
      <td>1.89</td>
      <td>Pharithdil38</td>
      <td>10-14</td>
      <td>1.89</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Splitter, Foe Of Subtlety</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>4.15</td>
      <td>Aeri79</td>
      <td>15-19</td>
      <td>4.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Storm-Weaver, Slayer of Inception</th>
      <td>23</td>
      <td>Female</td>
      <td>68</td>
      <td>4.39</td>
      <td>Firon67</td>
      <td>15-19</td>
      <td>4.39</td>
      <td>2.0</td>
      <td>8.78</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Stormcaller</th>
      <td>21</td>
      <td>Male</td>
      <td>180</td>
      <td>2.77</td>
      <td>Lisirra44</td>
      <td>15-19</td>
      <td>2.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Stormfury Longsword</th>
      <td>36</td>
      <td>Female</td>
      <td>173</td>
      <td>4.01</td>
      <td>Jiskim75</td>
      <td>30-34</td>
      <td>4.01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Swan Song, Gouger Of Terror</th>
      <td>24</td>
      <td>Male</td>
      <td>97</td>
      <td>1.92</td>
      <td>Chaniman66</td>
      <td>15-19</td>
      <td>1.92</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Thorn, Conqueror of the Corrupted</th>
      <td>8</td>
      <td>Male</td>
      <td>9</td>
      <td>1.42</td>
      <td>Aiduecal76</td>
      <td>NaN</td>
      <td>1.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Thunderfury Scimitar</th>
      <td>38</td>
      <td>Male</td>
      <td>163</td>
      <td>4.16</td>
      <td>Ardcil81</td>
      <td>30-34</td>
      <td>4.16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Torchlight, Bond of Storms</th>
      <td>20</td>
      <td>Male</td>
      <td>18</td>
      <td>3.75</td>
      <td>Eollym91</td>
      <td>15-19</td>
      <td>3.75</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Trickster</th>
      <td>21</td>
      <td>Male</td>
      <td>31</td>
      <td>4.59</td>
      <td>Jiskjask76</td>
      <td>15-19</td>
      <td>4.59</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Twilight's Carver</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>10-14</td>
      <td>2.55</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Undead Crusader</th>
      <td>20</td>
      <td>Male</td>
      <td>134</td>
      <td>2.15</td>
      <td>Syalallodil59</td>
      <td>15-19</td>
      <td>2.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Verdict</th>
      <td>39</td>
      <td>Female</td>
      <td>2</td>
      <td>2.65</td>
      <td>Aesririam61</td>
      <td>30-34</td>
      <td>2.65</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>War-Forged Gold Deflector</th>
      <td>21</td>
      <td>Male</td>
      <td>155</td>
      <td>4.04</td>
      <td>Heulaedru70</td>
      <td>15-19</td>
      <td>4.04</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Warmonger, Gift of Suffering's End</th>
      <td>40</td>
      <td>Male</td>
      <td>148</td>
      <td>4.65</td>
      <td>Aerithllora36</td>
      <td>35-39</td>
      <td>4.65</td>
      <td>1.0</td>
      <td>4.65</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Wolf</th>
      <td>30</td>
      <td>Male</td>
      <td>60</td>
      <td>2.70</td>
      <td>Sundaky74</td>
      <td>25-29</td>
      <td>2.70</td>
      <td>1.0</td>
      <td>2.70</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>63 rows × 10 columns</p>
</div>




```python
#Most Profitable Items
#Identify the 5 most profitable items by total purchase value, then list (in a table):

purchase_value_groups_df = purchase_data_2_pd.groupby("Item Name")
purchase_value_groups_df.max()

#purchase_value_groups_df.sort_values([Total Purchase Value])
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>SN</th>
      <th>categories</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Counts</th>
      <th>Total Purchase Value</th>
      <th>Purchase Counts_by_Item Name</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alpha, Oath of Zeal</th>
      <td>17</td>
      <td>Male</td>
      <td>79</td>
      <td>1.31</td>
      <td>Yarmol79</td>
      <td>10-14</td>
      <td>1.31</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Apocalyptic Battlescythe</th>
      <td>35</td>
      <td>Male</td>
      <td>93</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>30-34</td>
      <td>4.49</td>
      <td>1.0</td>
      <td>4.49</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Arcane Gem</th>
      <td>25</td>
      <td>Male</td>
      <td>84</td>
      <td>4.81</td>
      <td>Eusty71</td>
      <td>20-24</td>
      <td>4.81</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Betrayer</th>
      <td>21</td>
      <td>Male</td>
      <td>90</td>
      <td>4.12</td>
      <td>Lirtassa77</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>1.0</td>
      <td>4.12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Blade of the Grave</th>
      <td>16</td>
      <td>Male</td>
      <td>172</td>
      <td>2.71</td>
      <td>Shaidanu32</td>
      <td>10-14</td>
      <td>2.71</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Bloodlord's Fetish</th>
      <td>24</td>
      <td>Male</td>
      <td>4</td>
      <td>1.91</td>
      <td>Airi27</td>
      <td>15-19</td>
      <td>1.91</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Bonecarvin Battle Axe</th>
      <td>8</td>
      <td>Male</td>
      <td>44</td>
      <td>4.36</td>
      <td>Yarith71</td>
      <td>NaN</td>
      <td>4.36</td>
      <td>1.0</td>
      <td>4.36</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Celeste</th>
      <td>23</td>
      <td>Male</td>
      <td>91</td>
      <td>2.92</td>
      <td>Iskossaya95</td>
      <td>15-19</td>
      <td>2.92</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Crucifer</th>
      <td>32</td>
      <td>Male</td>
      <td>23</td>
      <td>3.67</td>
      <td>Palyon91</td>
      <td>25-29</td>
      <td>3.67</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Darkheart, Butcher of the Champion</th>
      <td>20</td>
      <td>Male</td>
      <td>158</td>
      <td>1.94</td>
      <td>Lassimla92</td>
      <td>15-19</td>
      <td>1.94</td>
      <td>1.0</td>
      <td>1.94</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Dawne</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>15-19</td>
      <td>3.36</td>
      <td>1.0</td>
      <td>3.36</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Deadline, Voice Of Subtlety</th>
      <td>25</td>
      <td>Male</td>
      <td>98</td>
      <td>1.29</td>
      <td>Undadar97</td>
      <td>20-24</td>
      <td>1.29</td>
      <td>1.0</td>
      <td>1.29</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Demise</th>
      <td>17</td>
      <td>Male</td>
      <td>71</td>
      <td>3.09</td>
      <td>Ilara98</td>
      <td>10-14</td>
      <td>3.09</td>
      <td>1.0</td>
      <td>3.09</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Exiled Doomblade</th>
      <td>24</td>
      <td>Male</td>
      <td>164</td>
      <td>1.31</td>
      <td>Chaniman66</td>
      <td>15-19</td>
      <td>1.31</td>
      <td>2.0</td>
      <td>2.62</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Exiled Mithril Longsword</th>
      <td>34</td>
      <td>Male</td>
      <td>126</td>
      <td>1.08</td>
      <td>Jiskimsda56</td>
      <td>25-29</td>
      <td>1.08</td>
      <td>1.0</td>
      <td>1.08</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>21</td>
      <td>Male</td>
      <td>108</td>
      <td>2.26</td>
      <td>Pheodaisun84</td>
      <td>15-19</td>
      <td>2.26</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fate, Vengeance of Eternal Justice</th>
      <td>33</td>
      <td>Male</td>
      <td>129</td>
      <td>2.88</td>
      <td>Ethralan59</td>
      <td>25-29</td>
      <td>2.88</td>
      <td>1.0</td>
      <td>2.88</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Feral Katana</th>
      <td>23</td>
      <td>Male</td>
      <td>154</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>15-19</td>
      <td>4.11</td>
      <td>1.0</td>
      <td>4.11</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fury</th>
      <td>11</td>
      <td>Male</td>
      <td>131</td>
      <td>2.99</td>
      <td>Eoralphos86</td>
      <td>&lt;10</td>
      <td>2.99</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fusion Pummel</th>
      <td>25</td>
      <td>Male</td>
      <td>64</td>
      <td>2.42</td>
      <td>Undirrasta74</td>
      <td>20-24</td>
      <td>2.42</td>
      <td>1.0</td>
      <td>2.42</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Ghost Reaver, Longsword of Magic</th>
      <td>23</td>
      <td>Female</td>
      <td>118</td>
      <td>2.95</td>
      <td>Assistast50</td>
      <td>15-19</td>
      <td>2.95</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Gladiator's Glaive</th>
      <td>20</td>
      <td>Male</td>
      <td>104</td>
      <td>1.84</td>
      <td>Ila44</td>
      <td>15-19</td>
      <td>1.84</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hailstorm Shadowsteel Scythe</th>
      <td>30</td>
      <td>Female</td>
      <td>105</td>
      <td>1.02</td>
      <td>Undosian34</td>
      <td>25-29</td>
      <td>1.02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Heartseeker, Reaver of Souls</th>
      <td>25</td>
      <td>Male</td>
      <td>127</td>
      <td>1.34</td>
      <td>Lirtastan49</td>
      <td>20-24</td>
      <td>1.34</td>
      <td>1.0</td>
      <td>1.34</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Heartstriker, Legacy of the Light</th>
      <td>25</td>
      <td>Male</td>
      <td>117</td>
      <td>4.71</td>
      <td>Sundaky74</td>
      <td>20-24</td>
      <td>4.71</td>
      <td>1.0</td>
      <td>4.71</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hero Cane</th>
      <td>18</td>
      <td>Male</td>
      <td>25</td>
      <td>4.78</td>
      <td>Chanirra64</td>
      <td>10-14</td>
      <td>4.78</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hope's End</th>
      <td>23</td>
      <td>Male</td>
      <td>70</td>
      <td>4.28</td>
      <td>Heosurnuru52</td>
      <td>15-19</td>
      <td>4.28</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Lazarus, Terror of the Earth</th>
      <td>33</td>
      <td>Male</td>
      <td>17</td>
      <td>1.96</td>
      <td>Chanjasksda31</td>
      <td>25-29</td>
      <td>1.96</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Malice, Legacy of the Queen</th>
      <td>15</td>
      <td>Male</td>
      <td>167</td>
      <td>3.25</td>
      <td>Heudai45</td>
      <td>10-14</td>
      <td>3.25</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mercy, Katana of Dismay</th>
      <td>36</td>
      <td>Male</td>
      <td>139</td>
      <td>4.25</td>
      <td>Aesurstilis64</td>
      <td>30-34</td>
      <td>4.25</td>
      <td>1.0</td>
      <td>4.25</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Orbit</th>
      <td>11</td>
      <td>Female</td>
      <td>41</td>
      <td>3.85</td>
      <td>Isristira52</td>
      <td>&lt;10</td>
      <td>3.85</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Peacekeeper, Wit of Dark Magic</th>
      <td>32</td>
      <td>Male</td>
      <td>138</td>
      <td>2.63</td>
      <td>Hairith93</td>
      <td>25-29</td>
      <td>2.63</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Possessed Core</th>
      <td>20</td>
      <td>Male</td>
      <td>14</td>
      <td>2.82</td>
      <td>Frichilsa31</td>
      <td>15-19</td>
      <td>2.82</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Primitive Blade</th>
      <td>24</td>
      <td>Male</td>
      <td>174</td>
      <td>1.36</td>
      <td>Zhisrisu83</td>
      <td>15-19</td>
      <td>1.36</td>
      <td>1.0</td>
      <td>1.36</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Purgatory, Gem of Regret</th>
      <td>8</td>
      <td>Male</td>
      <td>8</td>
      <td>2.22</td>
      <td>Hainaria90</td>
      <td>NaN</td>
      <td>2.22</td>
      <td>1.0</td>
      <td>2.22</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Putrid Fan</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>10-14</td>
      <td>2.63</td>
      <td>1.0</td>
      <td>2.63</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Reaper's Toll</th>
      <td>23</td>
      <td>Male</td>
      <td>181</td>
      <td>4.12</td>
      <td>Yarithrgue83</td>
      <td>15-19</td>
      <td>4.12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Relentless Iron Skewer</th>
      <td>23</td>
      <td>Other / Non-Disclosed</td>
      <td>176</td>
      <td>2.12</td>
      <td>Inadeu25</td>
      <td>15-19</td>
      <td>2.12</td>
      <td>1.0</td>
      <td>2.12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Restored Bauble</th>
      <td>21</td>
      <td>Male</td>
      <td>16</td>
      <td>2.15</td>
      <td>Chrathybust28</td>
      <td>15-19</td>
      <td>2.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Riddle, Tribute of Ended Dreams</th>
      <td>28</td>
      <td>Male</td>
      <td>27</td>
      <td>3.38</td>
      <td>Undirra90</td>
      <td>20-24</td>
      <td>3.38</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Rusty Skull</th>
      <td>24</td>
      <td>Male</td>
      <td>6</td>
      <td>3.58</td>
      <td>Lisosiast26</td>
      <td>15-19</td>
      <td>3.58</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Shadowsteel</th>
      <td>20</td>
      <td>Female</td>
      <td>170</td>
      <td>1.74</td>
      <td>Sondassasya91</td>
      <td>15-19</td>
      <td>1.74</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Sleepwalker</th>
      <td>35</td>
      <td>Male</td>
      <td>10</td>
      <td>1.81</td>
      <td>Streural92</td>
      <td>30-34</td>
      <td>1.81</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Soul-Forged Steel Shortsword</th>
      <td>9</td>
      <td>Male</td>
      <td>156</td>
      <td>4.53</td>
      <td>Rarallo90</td>
      <td>NaN</td>
      <td>4.53</td>
      <td>1.0</td>
      <td>4.53</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Splinter</th>
      <td>16</td>
      <td>Female</td>
      <td>0</td>
      <td>1.89</td>
      <td>Pharithdil38</td>
      <td>10-14</td>
      <td>1.89</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Splitter, Foe Of Subtlety</th>
      <td>23</td>
      <td>Female</td>
      <td>107</td>
      <td>4.15</td>
      <td>Aeri79</td>
      <td>15-19</td>
      <td>4.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Storm-Weaver, Slayer of Inception</th>
      <td>23</td>
      <td>Female</td>
      <td>68</td>
      <td>4.39</td>
      <td>Firon67</td>
      <td>15-19</td>
      <td>4.39</td>
      <td>2.0</td>
      <td>8.78</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Stormcaller</th>
      <td>21</td>
      <td>Male</td>
      <td>180</td>
      <td>2.77</td>
      <td>Lisirra44</td>
      <td>15-19</td>
      <td>2.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Stormfury Longsword</th>
      <td>36</td>
      <td>Female</td>
      <td>173</td>
      <td>4.01</td>
      <td>Jiskim75</td>
      <td>30-34</td>
      <td>4.01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Swan Song, Gouger Of Terror</th>
      <td>24</td>
      <td>Male</td>
      <td>97</td>
      <td>1.92</td>
      <td>Chaniman66</td>
      <td>15-19</td>
      <td>1.92</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Thorn, Conqueror of the Corrupted</th>
      <td>8</td>
      <td>Male</td>
      <td>9</td>
      <td>1.42</td>
      <td>Aiduecal76</td>
      <td>NaN</td>
      <td>1.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Thunderfury Scimitar</th>
      <td>38</td>
      <td>Male</td>
      <td>163</td>
      <td>4.16</td>
      <td>Ardcil81</td>
      <td>30-34</td>
      <td>4.16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Torchlight, Bond of Storms</th>
      <td>20</td>
      <td>Male</td>
      <td>18</td>
      <td>3.75</td>
      <td>Eollym91</td>
      <td>15-19</td>
      <td>3.75</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Trickster</th>
      <td>21</td>
      <td>Male</td>
      <td>31</td>
      <td>4.59</td>
      <td>Jiskjask76</td>
      <td>15-19</td>
      <td>4.59</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Twilight's Carver</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>10-14</td>
      <td>2.55</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Undead Crusader</th>
      <td>20</td>
      <td>Male</td>
      <td>134</td>
      <td>2.15</td>
      <td>Syalallodil59</td>
      <td>15-19</td>
      <td>2.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Verdict</th>
      <td>39</td>
      <td>Female</td>
      <td>2</td>
      <td>2.65</td>
      <td>Aesririam61</td>
      <td>30-34</td>
      <td>2.65</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>War-Forged Gold Deflector</th>
      <td>21</td>
      <td>Male</td>
      <td>155</td>
      <td>4.04</td>
      <td>Heulaedru70</td>
      <td>15-19</td>
      <td>4.04</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Warmonger, Gift of Suffering's End</th>
      <td>40</td>
      <td>Male</td>
      <td>148</td>
      <td>4.65</td>
      <td>Aerithllora36</td>
      <td>35-39</td>
      <td>4.65</td>
      <td>1.0</td>
      <td>4.65</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Wolf</th>
      <td>30</td>
      <td>Male</td>
      <td>60</td>
      <td>2.70</td>
      <td>Sundaky74</td>
      <td>25-29</td>
      <td>2.70</td>
      <td>1.0</td>
      <td>2.70</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>63 rows × 10 columns</p>
</div>




```python


```
