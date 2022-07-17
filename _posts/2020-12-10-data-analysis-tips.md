---
layout: post
title: 10 tips for data analysis
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Machine Learning, Python, Pandas]
---

In this blog we'll discuss about few techniques while doing data analysis.

# 1. Check for null values

Once we read the dataset, we should always check for null values. Following line of code can be used for it:

`df.isnull().sum(axis=0)`

It gives the total number of null values for each column in the dataset.

# 2. Check for duplicate values

We can check whether there are duplicate values in the dataset using the following command:

`df.duplicated().sum()`

It gives us the total number of duplicated rows. We can drop using following command:

`df.drop_duplicates(keep=False)`

# 3. Check for unique values

It is useful for categorical data. Number of unique values can be checked in a particular column using following code:

`df['column_name'].unique()`

# 4. Replace/Drop Null values

Dealing with null values is also very important for data analysis. We can either remove the column if there are too many null values

`df['column_name'].dropna(inplace=True)`

or we can impute them with mean/median/mode.

`df['column'].fillna(df['column'].mean(),inplace=True)`

# 5. Correlation Matrix

It gives us the information about the correlation between different features. Following command can be used for it:

```
import seaborn as sns
corrmat = df.corr()
f, ax = plt.subplots(figsize=(12, 9))
sns.heatmap(corrmat, square=True);
```

We are using seaborn package to plot the matrix.

# 6. Check distribution of a variable

We can also check for the distribution of a particular column. By plot we can understand whether the data is following a normal distribution or some other. Following is the command:

```
import seaborn as sns
sns.distplot(df['column'])
```

# 7. Check datatypes of columns

We can check the datatype of columns in the data. It helps us to confirm whether data is having correct data type or not.

`df.dtypes`

# 8. Deal with datetime columns

Many times we get dates in a column but not in datetime format. We can convert it into one by using following code:

`df["Date.of.Birth"] = df['Date.of.Birth'].astype('datetime64[ns]')`

# 9. Value count

We can check the frequency of different categories in a categorical column:

`df['column'].value_counts()` 

# 10. Max/Min value of a column

We can find out the maximum and minimum values in a particular column using max() and min() command:

`df['column'].max()`
`df['column'].max()`

You can checkout my sample notebook with all these commands in action with a dataset.

[Jupyter Notebook](https://www.kaggle.com/anu0012/startup-funding-dataset-visualization)

That's it for now. Next time we'll try to find out some more tips and tricks for data analysis. :)

