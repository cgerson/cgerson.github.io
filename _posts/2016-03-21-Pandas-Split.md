---
layout: post
title: Pandas Split
---

I use the open source <a href="http://pandas.pydata.org/">Python pandas library</a> frequently for data processing and analysis and plotting and all the things. 

A function I use often is the GroupBy function, which pandas creator Wes Mckinney defines as a method to "split-apply-combine". It allows the user to split the data into subsets according to values in a selected array, apply some function on each separate subset, then combine all the data back into an object with the aggregated values.

In essence, we're performing a map-reduce, where the first two steps (split & apply) are the mapping step and the last step (combine) is the reduce step.

Alright. But the reason I'm writing this lightning post is to share excitement about a functionality of GroupBy I had never seen before.

Here goes.

My use case: I'll often have a dataset which I'll want to subset according to values in one or more columns, and manipulate each of the subsets individually.

Groupby solution: Create a dictionary from the GroupBy object!

Example:
- Data: unemployment rates from Spain, by year (2013-2015) and quartile (1-4). Here are the first 10 rows:
<table border="1" class="dataframe">\n  <thead>\n    <tr style="text-align: right;">\n      <th></th>\n      <th>Year</th>\n      <th>Quartile</th>\n      <th>Age</th>\n      <th>Unemployment Rate</th>\n    </tr>\n  </thead>\n  <tbody>\n    <tr>\n      <th>0</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>16-19</td>\n      <td>66.09</td>\n    </tr>\n    <tr>\n      <th>1</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>20-24</td>\n      <td>42.52</td>\n    </tr>\n    <tr>\n      <th>2</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>25-29</td>\n      <td>27.57</td>\n    </tr>\n    <tr>\n      <th>3</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>30-34</td>\n      <td>20.25</td>\n    </tr>\n    <tr>\n      <th>4</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>35-39</td>\n      <td>17.73</td>\n    </tr>\n    <tr>\n      <th>5</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>40-44</td>\n      <td>17.29</td>\n    </tr>\n    <tr>\n      <th>6</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>45-49</td>\n      <td>18.76</td>\n    </tr>\n    <tr>\n      <th>7</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>50-54</td>\n      <td>17.77</td>\n    </tr>\n    <tr>\n      <th>8</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>55-59</td>\n      <td>19.14</td>\n    </tr>\n    <tr>\n      <th>9</th>\n      <td>2015</td>\n      <td>4</td>\n      <td>60-64</td>\n      <td>16.74</td>\n    </tr>\n  </tbody>\n</table>

- Let's say I want to subset the data by year. There are a few ways to do this in pandas, but with GroupBy... ONE ELEGANT LINE:
```python
year_subsets = dict(list(new_df.groupby('Year')))
```
- `year subsets` is a dictionary whose keys are years (2013, 2014, 2015) and whose values are DataFrames of rows from said year.

There are alternative ways to subset data in pandas, but this is the only one-liner I've seen that returns the data in the original format with its original indices.
