---
layout: post
title: Citimodels
---

Bikeshare programs around the country have seen varied levels of success. These programs, some developed publicly and others privately owned, have recently released their data in hopes that inspired and/or bored data-nerds will take an interest and analyze.

<a href="http://www.citibikenyc.com/system-data" target="_blank">New York</a>, <a href="http://www.bayareabikeshare.com/datachallenge" target="_blank">Bay Area</a>, <a href="https://www.divvybikes.com/datachallenge" target="_blank">Chicago</a>, <a href="http://www.capitalbikeshare.com/system-data" target="_blank">Washington DC</a>, to name four, have opened up challenges. And, as hoped, some really cool people have produced some really cool things since the data release.

And I wanted in!

## CitiData

This is the dataset belonging to the New York City bikeshare program, Citibike.

Each observation (row) is a bike trip from station A to station B. Other features include a timestamp, lat/long of stations, bike id, trip duration, and gender and birth year (if user was a subscriber).

I looked concretely at three months of data: from Dec 1st 2014 until Feb 28th 2015. This data contained over 800 thousand bike trips, over five thousand unique bikes and 329 Citibike stations.

Data thoughts: Great dataset. Really clean. Some expected datatype conversions needed. Some bike trips passed the 24 hour mark, and a few users with birth years before 1900. Grandpas stealing bikes, no doubt.

## CitiFeatureExtraction

So many bike going every which way! I wondered: <b>can I classify (predict) the destination neighborhood of the departing bike trip?</b>

First I mapped each of the 329 bike stations to its legally defined neighborhood in Manhattan or Brooklyn with the following tools:
* <a href="http://catalog.opendata.city/dataset/pediacities-nyc-neighborhoods/resource/91778048-3c58-449c-a3f9-365ed203e914" target="_blank">GeoJSON file of NYC bounderies</a>
* station data provided by Citibike
* CartoDB's <a href="http://docs.cartodb.com/tips-and-tricks.html#spatial-intersection-of-two-tables" target="_blank">SQL geographic join feature</a>, in which I could overlay the stations on the boundaries map and assign each station to its associated neighborhood.

This way 329 stations could be reduced to 37 neighborhoods.

I removed all non-subscribers (less than 3% of dataset) and could then <b>use the following features: starting neighborhood (1 of 37), time of day, day of the week, gender and birth year</b>.

## CitiClassificationModelling

Predicting one of 37 classes is complicated with such sparse data: each trip began from only ONE of 37 points, ONE day of the week of 7, ONE gender, then birth year and starting time. Therefore, each trip had data for only 5 of 48 total features! My best models reached an average prediction accuracy of no more than .28 (out of 1).

In this <a href="http://cgerson.github.io/adopt-a-bike-model/" target="_blank">graph</a> we can see which features had the greatest relative importance in the model. 

## CitiAdopt

Why were we predicting the destination neighborhood again? Mainly to play with classification models, to be honest. The value of knowing where one user from point A ends up could be interesting for developing bike infrastructure along certain paths, but more suitable than a prediction model is a model of average traffic patters. Most users are commuters, and their commute is more or less constant.

Therefore, I imagined creating an app for sponsors of the bikeshare program. These sponsors would adopt a bike with a contribution (something like when Kramer adopted that highway) and would interact with their bike via an app, which would allow the user to "predict" its route. Putting the "fun" back in fundraising.

Here I created the app's <a href = "http://cgerson.github.io/adopt-a-bike/">proposed interface</a> showing:
* the home screen: a map of NYC with the bike as a dot, hopping around, and
* a notification of pickup: giving the sponsor 30 seconds to guess its destination

## CitiPowerpoint

Check out the slides for graphs

<iframe src="//slides.com/claireger/deck-3/embed" width="576" height="420" scrolling="no" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>