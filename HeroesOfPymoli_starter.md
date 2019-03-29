
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# File to Load (Remember to Change These)
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)
```


```python
purchase_data.head()
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
      <th>Purchase ID</th>
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
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
#Counting the number of Unique SN
NumberOfPlayers = len(purchase_data["SN"].unique())

#creating a Data Frame (df) for the number of players
NumberOfPlayers_df = pd.DataFrame({"Total Players": [NumberOfPlayers]})

#printing the df
NumberOfPlayers_df
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
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
#Counting the number of unique Items 
UniqueItems = len(purchase_data["Item ID"].unique())


AveragePrice = purchase_data["Price"].mean()

NumberOfPurchases = len(purchase_data["Item Name"])

TotalRevenue = purchase_data["Price"].sum()

#The format for the df
pd.options.display.float_format = "${:,.2f}".format

#creating a df using the values above
PurchaseSummary_df = pd.DataFrame({"Number of Unique Items": [UniqueItems],
        "Average Price": [AveragePrice],
        "Number of Purchases": [NumberOfPurchases],
        "Total Revenue": [TotalRevenue]})

#printing the df
PurchaseSummary_df
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
      <td>$3.05</td>
      <td>780</td>
      <td>$2,379.77</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
#df showing one record for each player
UniquePlayers_df=purchase_data.drop_duplicates(["SN"])

#counts for each category
MaleCount= UniquePlayers_df["Gender"].value_counts()["Male"]
FemaleCount= UniquePlayers_df["Gender"].value_counts()["Female"]
OtherCount=NumberOfPlayers-MaleCount-FemaleCount

#Percentages for each category
MalePercent = ((MaleCount/NumberOfPlayers)*100)
FemalePercent = ((FemaleCount/NumberOfPlayers)*100)
OtherPercent = ((OtherCount/NumberOfPlayers)*100)

#creating a df using the values above
Gender_df = pd.DataFrame({"": ["Male", "Female", "Other/Non-Disclosed"],
                          "Total Count": [MaleCount, FemaleCount, OtherCount], 
                          "Percentage of Players": [MalePercent, FemalePercent, OtherPercent]})
#formatting the df          
pd.options.display.float_format = "{:.2f}".format

#setting gender as an index for the df
GenderIndexed_df = Gender_df.set_index("")

#printing the df
GenderIndexed_df           

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
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#creating an object categorized by gender on the one to many df
PurchaseCountByGender=purchase_data.groupby(["Gender"])

#creating an object categorized by gender on the one to one df
PurchaseCountByGenderUnique=UniquePlayers_df.groupby(["Gender"])

#creating Lists/arrays for each column
PurchaseCount=list(PurchaseCountByGender.count()["Purchase ID"])
AvgPurchasePrice=list(PurchaseCountByGender.mean()["Price"])
TPurchaseValue=list(PurchaseCountByGender.sum()["Price"])
AvgTPurchaseValuepp=list(PurchaseCountByGender.sum()["Price"]/PurchaseCountByGenderUnique.count()["Purchase ID"])

#formatting the df  
pd.options.display.float_format = "${:,.2f}".format

#creating a df using the values above
GenderPurchase_df = pd.DataFrame({"Gender": ["Male", "Female", "Other/Non-Disclosed"],
                          "Purchase Count": PurchaseCount,"Average Purchase Price":AvgPurchasePrice,
                            "Total Purchase Value":TPurchaseValue,"Avg Total Purchase per Person":AvgTPurchaseValuepp})

#setting gender as an index for the df
GenderPurchaseIndexed_df = GenderPurchase_df.set_index("Gender")

#printing the df
GenderPurchaseIndexed_df
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
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$4.47</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$1,967.64</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$4.56</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
#creating cut_off points which do not includ the right limit
bins = [0, 10, 15, 20, 25,30,35,40,50]
labels =["<10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]

#Adding a column showing age categories to the df with unique players
UniquePlayers_df["AgeCategories"] = pd.cut(UniquePlayers_df["Age"], bins,labels=labels,right=False)

#creating an object categorized by Age categories on the one to one df
CountByAgeCategory=UniquePlayers_df.groupby(["AgeCategories"])

#creating Lists/arrays for each column
NumberInEachCategory=list(CountByAgeCategory.count()["Purchase ID"])
PercentInEachCategory=list(CountByAgeCategory.count()["Purchase ID"]/len(purchase_data["SN"].unique())*100)

#formatting the df  
pd.options.display.float_format = "{:.2f}".format

#creating a df using the values above
AgeCategories_df = pd.DataFrame({"": labels,
                          "Total Count":NumberInEachCategory,"Percentage of Players":PercentInEachCategory})

#setting age category as an index for the df
AgeCategoriesIndexed_df = AgeCategories_df.set_index("")

#printing the df
AgeCategoriesIndexed_df
```

    C:\Users\farai\Anaconda3\lib\site-packages\ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    




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
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#Adding a column showing age categories to the df with purchases data
purchase_data["AgeCategories"] = pd.cut(purchase_data["Age"], bins,labels=labels,right=False)

#creating an object categorized by Age categories on the one to many df
PurchaseCountByAgecat=purchase_data.groupby(["AgeCategories"])

#creating Lists/arrays for each column
PurchaseCountAge=list(PurchaseCountByAgecat.count()["Purchase ID"])
AvgPurchasePriceAge=list(PurchaseCountByAgecat.mean()["Price"])
TotalPurchaseValueAge=list(PurchaseCountByAgecat.sum()["Price"])
AvgTPurchaseppAge=list(PurchaseCountByAgecat.sum()["Price"]/CountByAgeCategory.count()["Purchase ID"])

#formatting the df  
pd.options.display.float_format = "${:,.2f}".format

#creating a df using the values above
AgePurchase_df = pd.DataFrame({"": ["<10","10-14","15-19","20-24","25-29","30-34","35-39","40+"],
                          "Purchase Count": PurchaseCountAge,"Average Purchase Price": AvgPurchasePriceAge,
                        "Total Purchase Value":TotalPurchaseValueAge,"Avg Total Purchase per Person":AvgTPurchaseppAge})

#setting age category as an index for the df
AgePurchaseIndexed_df = AgePurchase_df.set_index("")

#re-arranging the Index to have the under 10 category as the las row
AgePurchaseReIndexed_df=AgePurchaseIndexed_df.reindex(["10-14","15-19","20-24","25-29","30-34","35-39","40+","<10"])

#printing the df
AgePurchaseReIndexed_df
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
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$3.76</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$4.12</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$4.76</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$3.19</td>
    </tr>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
#creating an object categorized by Serial Number on the one to many df
PurchaseCountBySN=purchase_data.groupby(["SN"])

#creating a df from the dictionary with count information
SNPurchases_df=pd.DataFrame.from_dict(PurchaseCountBySN.count()["Purchase ID"])

#creating Lists/arrays for each column
TotalPurchaseValueSN=list(PurchaseCountBySN.sum()["Price"])
AvgPurchasePriceSN=list(PurchaseCountBySN.sum()["Price"]/PurchaseCountBySN.count()["Purchase ID"])

#adding columns to the data frame using the above arrays
SNPurchases_df["Average Purchase Price"]=TotalPurchaseValueSN
SNPurchases_df["Total Purchase Value"]=TotalPurchaseValueSN

#formatting the df  
pd.options.display.float_format = "${:,.2f}".format

#renaming the count column and keeping the original df
SNPurchases_df.rename(columns={"Purchase ID":"Purchase Count"}, inplace=True)

#Descending sort by Total Purchase Value
SNPurchasesSorted_df=SNPurchases_df.sort_values("Total Purchase Value", ascending=False)

#printing the df
SNPurchasesSorted_df.head()

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
      <th>Average Purchase Price</th>
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
      <th>Lisosia93</th>
      <td>5</td>
      <td>$18.96</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$15.45</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$13.83</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$13.62</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$13.10</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
#creating an object categorized by Item ID on the one to many df
PurchaseCountByItem=purchase_data.groupby(["Item ID"])

#creating a df from the dictionary with count information
ItemPurchases_df=pd.DataFrame.from_dict(PurchaseCountByItem.count()["Purchase ID"])

#creating Lists/arrays for each column
PriceIID=list(PurchaseCountByItem.first()["Price"])
TotalPurchaseValueIID=list(PurchaseCountByItem.sum()["Price"])
NameIID=list(PurchaseCountByItem.first()["Item Name"])

#Adding columns to the df
ItemPurchases_df["Item Name"]=NameIID
ItemPurchases_df["Item Price"]=PriceIID
ItemPurchases_df["Total Purchase Value"]=TotalPurchaseValueIID

#formatting the df  
pd.options.display.float_format = "${:,.2f}".format

#renaming the count column and keeping the original df
ItemPurchases_df.rename(columns={"Purchase ID":"Purchase Count"}, inplace=True)

#Descending sort by Purchase Count
ItemPurchasesSorted_df=ItemPurchases_df.sort_values("Purchase Count", ascending=False)

#Adding Item names as another index to Item ID
ItemPurchasesSortedIndexed_df=ItemPurchasesSorted_df.set_index(["Item Name"],append=True)

#printing the df
ItemPurchasesSortedIndexed_df.head()
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>19</th>
      <th>Pursuit, Cudgel of Necromancy</th>
      <td>8</td>
      <td>$1.02</td>
      <td>$8.16</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
#Using the above df and sorting by Total Purchase Value
ItemPurchasesSortedTPVIndexed_df=ItemPurchasesSortedIndexed_df.sort_values("Total Purchase Value", ascending=False)
ItemPurchasesSortedTPVIndexed_df.head()
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>8</td>
      <td>$4.88</td>
      <td>$39.04</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>


