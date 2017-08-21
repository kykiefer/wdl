Below I write code in Python by interacting with two modules — pandas and seaborn. [Pandas](http://pandas.pydata.org/) is an Excel-like module for big data and enhanced manipulation. [Seaborn](https://seaborn.pydata.org/) is a tool for creating beautiful charts and visuals. If you gain comfort with Python and these modules, machine learning is not far away (look to a module called [scikit-learn](http://scikit-learn.org/stable/) and [this tutorial](http://scikit-learn.org/stable/tutorial/basic/tutorial.html) to get started).


```python
# import helpful modules
import pandas as pd # pd is an alias we can reference to call pandas in our code
import seaborn as sns

# load the Excel file
xlsx = pd.ExcelFile('FracStats_JobList_Summer2017.xlsx')
# load the selected tab from the Excel workbook into a pandas dataframe
df_frac = xlsx.parse('FracStats')

# print the first five rows of the data frame
print(df_frac.head())
```

<img alt="dataframe" src="img/df2.png" width='775'>

```python
# narrow down to stages treated with 'Gel' and not  screened out
df_gel = df_frac.loc[(df_frac['Fluid Type'] == 'Gel') & (df_frac['Screen Out'] == 'No')]

print("{} stages across {} wells.".format(df_gel.shape[0], len(df_gel['Well'].unique())))
```

`590 stages across 22 wells.`

```python
# plot the distribution of total sand pumped by formation in a box plot.
df_gel.boxplot(column='Total Proppant [lbs].1', by='Formation')
```

```python
# violin plot
sns.violinplot(data=df_gel, x="Formation", y="Total Proppant [lbs].1")
```
<img alt="violin plot" src="img/example.png" width='775'>
