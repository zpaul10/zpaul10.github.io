---
layout: post
title:      "Kings County Heatmap"
date:       2020-10-01 02:10:51 +0000
permalink:  kings_county_heatmap
---


I'm going to be working on a heatmap of the correlation between featires of Kings County housing market from 2014 to 2015, and showing how I made it. 

I start off with reading in the csv as a pandas dataframe and displaying the head. For the purposes of this demonstartion I'm not going to show every column because there are too many to list out, but it'd look a little something like this. 
```
import pandas as pd
file_name = 'kc_house_data.csv'
df = pd.read_csv(file_name, index_col = 0)
df.head()
```

| ID | Price | Zipcode | Grade |
| -------- | -------- | -------- | -------- |
| 7129300520     | 221900      | 98178     | 7|
| 6414100192    | 538000   | 98125   | 7|
| 5631500400     | 180000      | 98028     | 6|
| 2487200875   | 604000   | 98136  |7|
| 1954400510     | 510000      | 98074     |8|

The next step is simple, I just need to create the plot. I'm actually creating two plots at once here, one is a blank plot to overlay the top/right half, and the second is the actual plot we want to show. I am doing it like this to since the plot would normally mirror itself over the diagonal. Seeing the plot itself will have it make more sense. 

```
import seaborn as sns
df_corr = df.corr()

for i in range(len(df_corr)):
    for j in list(range(i,len(df_corr))):
        df_corr.iloc[i][j] = None
        
plt.figure(figsize = (20, 14))
sns.heatmap(df_corr, annot = True, center = 0)
```

![Correlation Plot Heatmap](https://imgur.com/a/pceVDbA)

There's a lot here though, and its not always going to be easy to pick out pairs that have high colinearity, especially as the number of features increases. So there's another, text based way, and I find that I prefer this option over the plot.

This does the same thing as the correlation plot previously, except in table form. It grabs the feature correlations, drops the duplicates (the ones that would be mirrored over the diagonal in the plot), and returns a dataframe containing only the pairs that have a colinearity factor that falls between the values we chose. In this case, greater than 0.75. Less than 1 is also included to avoid having things with perfect colinearity, features with themselves, which would fill up the dataframe with junk.
```
df_corr=df.corr().abs().stack().reset_index().sort_values(0, ascending=False)

df_corr['pairs'] = list(zip(df_corr.level_0, df_corr.level_1))

df_corr.set_index(['pairs'], inplace = True)

df_corr.drop(columns=['level_1', 'level_0'], inplace = True)

df_corr.columns = ['cc']

df_corr.drop_duplicates(inplace=True)

df_corr[(df_corr.cc > .75) & (df_corr.cc < 1)]
```

In this particular plot, there's a few. 

| ID | Price | 
| -------- | -------- | 
| (renovated, yr_renovated)    |0.999968     | 
| (yr_built, age)   | 0.926406  |
| (sqft_above, sqft_living)   | 0.876448     | 
| (sqft_living, grade)   | 0.762779   | 
| (sqft_living, sqft_living15)     | 0.756402      | 
| (sqft_above, grade)   | 0.756073   | 
| (sqft_living, bathrooms)   | 0.755758    | 

I can start with dropping a couple of these features if I wanted to make a linear model. For this particular dataset, I'd start with removing the following: yr_renovated, yr_built, sqft_above, grade, sqft_living15, and bathrooms. From there I could also look at VIF scores, or just start messing with a model and see what comes from it. 



