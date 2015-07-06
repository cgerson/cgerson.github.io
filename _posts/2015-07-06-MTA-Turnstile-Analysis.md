---
layout: post
title: MTA Turnstile Analysis
---

The first project assigned to us at Metis was based on <a href="http://web.mta.info/developers/turnstile.html" target="_blank">MTA Turnstile Data</a>.

Our task was to help fictional group WTWY in their efforts to optimize their street team in collecting emails from interested parties, in hopes of raising awareness of their organization and eventually <b>maximizing participation and financial contributions</b>.

The turnstile data includes entry and exit counts for each subway station, measured in four hour intervals at inconsistent times. Required significant man-hours to clean and organize the data. 

[Aside: At this point, I tried to avoid the wistful dreamy thinking of "hey, wouldn't it be great if the data were collected in a completely different way", because they weren't. This likely stems from my background in economics, where the worlds we analyze are perfect (i.e. "assume perfection...").]

![subway]({{ site.baseurl }}/images/Interested.png "Subway man")

My group proposed the following to the fictional client: an analysis of top stations with highest traffic during the workweek (divided into morning and evening traffic), as well a classification of stations in proximity to tech-related activity. Provided with both, the client could <b>optimize their efforts by deploying their street team at the locations with the greatest and most relevant audience</b>.

We presented the client with the following proof of concept, where red text are inputs that can be modified by the user.

![Design]({{ site.baseurl }}/images/MTA-POC.jpg "POC")