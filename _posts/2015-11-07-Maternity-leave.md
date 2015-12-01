---
layout: post
title: Maternity Leave by Industry
---

How many weeks of maternity leave do US industries offer their employees?

The website <a href = "https://fairygodboss.com/maternity-leave-resource-center" target="_blank">Fairygodboss</a> hosts a crowdsourced collection of maternity leave information. Each observation may include the name of the company, the industry, and the amount of paid and unpaid leave (in weeks) that the company offers.

This is a great example of important data that is not made public by companies or, if public, is fragmented. With crowdsourcing, individuals from disparate parts of the economy can come together and create a powerful and telling database. Yeehaw!

The code used to scrape and clean the data lives in this <a href = "https://github.com/cgerson/maternity-leave" target="_blank">GitHub repo</a>. The tools used were <a href="http://www.crummy.com/software/BeautifulSoup/">BeautifulSoup</a> (to scrape), <a href="http://pandas.pydata.org/">Pandas</a> (to manipulate the data) and some experiments with plotly (plotting).

Currently the dataset includes <b>891 companies</b> from <b>42 industries</b> (lastest update: December 01, 2015).

Average <b>paid leave</b> in weeks over all companies submitted is <b>8.0 weeks</b>.

Average <b>unpaid leave</b> is <b>8.7 weeks</b>.

Two outliers in this sample, <b>Bill and Melinda Gates Foundation</b> (Nonprofit) and <b>Netflix</b> (Technology), offer 52 weeks of paid maternity leave. 

Plotting the average leave offered by industry:<br>
(Note that companies that offer 0 weeks for either paid or unpaid are noted below. Otherwise only information currently available is displayed.)
<br><br>
<iframe width="750" height="900" frameborder="0" scrolling="no" src="https://plot.ly/~cgerson/66.embed"></iframe>
