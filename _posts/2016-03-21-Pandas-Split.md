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

**Groupby solution**: Create a dictionary from the GroupBy object!

Example:

* Unemployment data from Spain, by year (2013-2015) and quartile (1-4).
Here are the first 10 rows:

<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>Year</th>      <th>Quartile</th>      <th>Age</th>      <th>Unemployment Rate</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>2015</td>      <td>4</td>      <td>16-19</td>      <td>66.09</td>    </tr>    <tr>      <th>1</th>      <td>2015</td>      <td>4</td>      <td>20-24</td>      <td>42.52</td>    </tr>    <tr>      <th>2</th>      <td>2015</td>      <td>4</td>      <td>25-29</td>      <td>27.57</td>    </tr>    <tr>      <th>3</th>      <td>2015</td>      <td>4</td>      <td>30-34</td>      <td>20.25</td>    </tr>    <tr>      <th>4</th>      <td>2015</td>      <td>4</td>      <td>35-39</td>      <td>17.73</td>    </tr>    <tr>      <th>5</th>      <td>2015</td>      <td>4</td>      <td>40-44</td>      <td>17.29</td>    </tr>    <tr>      <th>6</th>      <td>2015</td>      <td>4</td>      <td>45-49</td>      <td>18.76</td>    </tr>    <tr>      <th>7</th>      <td>2015</td>      <td>4</td>      <td>50-54</td>      <td>17.77</td>    </tr>    <tr>      <th>8</th>      <td>2015</td>      <td>4</td>      <td>55-59</td>      <td>19.14</td>    </tr>    <tr>      <th>9</th>      <td>2015</td>      <td>4</td>      <td>60-64</td>      <td>16.74</td>    </tr>  </tbody></table>


Let's say I want to subset the data by year. There are a few ways to do this in pandas, but with GroupBy... ONE ELEGANT LINE:

`year_subsets = dict(list(new_df.groupby('Year')))`

The resulting `year_subsets` is a dictionary whose keys are years (2013, 2014, 2015) and whose values are DataFrames of rows from said year.

There are alternative ways to subset data in pandas, but this is the only one-liner I've seen that returns the data in the original format with its original indices.
