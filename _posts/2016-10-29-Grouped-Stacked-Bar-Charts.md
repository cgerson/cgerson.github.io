---
layout: post
title: Clusters of Stacked Bar Charts
---

Tis the season to visualize election polling data!

Today I sent in my absentee ballot (howdy, Texas) and set up a module to <b>chart survey results based on respondent demographic data</b>.

In particular, let's make a chart with Python's <a href="http://matplotlib.org/index.html">matplotlib</a> plotting library to see -- <b>which candidate are each gender and each age group leaning towards?</b> The module has got other applications, so I thought I'd share it here.

Its purpose is to be an out-of-the-box solution. Pass in a Pandas data object and the segments you wish to group by (i.e. columns in the dataframe), et voila!
<br>

```
clustered_stacked_chart.plot(electiondata,
                             my_two_segments=['Gender','Age'],
                             title = "Election Preferences by Gender and Age")
```


<img style= "width: 900;" src="http://cgerson.github.io/images/Election_Preferences_by_Gender_and_Age.png">
<br><br>


Find the GitHub source code <a href="https://github.com/cgerson/clustered-stacked-chart">here</a>.

And the Data Source here:

<a href="http://www.pewresearch.org/fact-tank/2016/07/28/a-closer-look-at-the-gender-gap-in-presidential-voting/ft_16-7-29-gender2/"><img width="310" height="696" src="http://assets.pewresearch.org/wp-content/uploads/sites/12/2016/07/FT_16.7.29.Gender2.png" class="attachment-large size-large" alt="2016 general election preferences among men and women" /></a>
