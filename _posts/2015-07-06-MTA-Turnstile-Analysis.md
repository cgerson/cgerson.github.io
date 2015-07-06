---
layout: post
title: MTA Turnstile Analysis
---

The first project assigned to us at Metis was based on <a href="http://web.mta.info/developers/turnstile.html" target="_blank">MTA Turnstile Data</a>.

Our task was to help fictional group WTWY in their efforts to optimize their street team in collecting emails from interested parties, in hopes of raising awareness of their organization and eventually <b>maximizing participation and financial contributions</b>.

The turnstile data includes total ridership for each subway station, measured in four hour intervals at inconsistent times. 

![subway]({{ site.baseurl }}/images/Interested.png "Subway man")

[Aside: At this point, I tried to avoid the wistful dreamy thinking of "hey, wouldn't it be great if the data were collected in a completely different way", because it wasn't. I come from a background in economics, where the worlds we analyze are perfect (i.e. "assume perfection...").]

My group proposed the following to the fictional client: an analysis of top stations with highest traffic during the workweek (divided into morning and evening traffic), as well a classification of stations in proximity to tech-related activity. Provided with both, the client could maximize their efforts by deploying their street team at the locations with the greatest and most relevant audience.

We presented the client with the following proof of concept, where red text are inputs that can be modified by the user.

![Design]({{ site.baseurl }}/images/MetisMTA.jpg "POC")