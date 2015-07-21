---
layout: post
title: Actors Analysis
---

My latest project at Metis sought to answer the following question: <b>Do adverse economic conditions early in an actor's life influence his/her relative success in the future?</b>

Answer: Probably not.


## Let me explain

(No time for explanations? Skip to ppt presentation below)

Thanks to my scrupulous efforts in <a href="http://cgerson.github.io/Webscraping/" target="_blank">webscraping</a>, I ended up with a nice, clean dataset of 617 observations. These were <b>617 unique actors</b>, all relatively successful given that they appeared on <a href="http://www.boxofficemojo.com/people/?view=Actor&sort=sumgross&adjust_yr=2015&p=.htm" target="_blank">Box Office Mojo's people index</a>.

However, studies have shown that young people who come of age in a recession tend to have <a href="http://www.epi.org/publication/bp243/" target="_blank">bleaker career prospects</a> in the long-term. The <a href="http://cgerson.github.io/thanks/" target="_blank">Mothers of Aspiring Millennial Actors</a> organization contacted me, worried. How true could this be in Hollywood?, they asked.

To find out, I created a model to measure how the economy in the past affected contemporary actors, and therefore have some sort of predictor for the millennials.


## Building the model: success defined

<img style= "width: 600px; border:3px solid black; margin: 0 auto;" src="http://cgerson.github.io/images/oscarrace.jpg"/>

I measured the actor's level of success by one metric: <b>the number of Oscar nominations received</b>.

I began by trying to predict the average gross of films featuring said actor, but the results were miserable. None of the features collected about the actor correlated with this variable (ergo, movie success is determined by more than one actor!). Ideally, I could have used income of actors as a measure, but I didn't find a reliable source of this data over time.


## Building the model: adverse economic conditions defined

To determine the health of the economy during various points in the actor's life, I used an <a href="https://research.stlouisfed.org/fred2/series/USREC" target="_blank">NBER-based recession indicator</a>. This dummy variable, measured monthly, assigns 1 to recessionary periods and 0 to expansionary periods. Using the actor's birthday, I could calculate the <b>number of recessionary months the actor was exposed to from ages 15-20 and 20-25</b>. (Here I am making the assumption that a US recession hits the global economy, in the case of foreign-born actors.) This measurement helps control for age, in that I am measuring the same length of time for every actor, regardless of age.


## Early findings

Some interesting information I pulled from the data.

The average age of (contemporary) Oscar nominees is 42.

<img style= "width: 500px; border:3px solid black; margin: 0 auto;" src="http://cgerson.github.io/images/Age_Osc.png"/>


Men and Oscar nominees have higher grossing films on average.

<img style= "width: 500px; border:3px solid black; margin: 0 auto;" src="http://cgerson.github.io/images/Avg_Gross_Sex_Osc.png"/>


Oscar nominees endured MORE economic recessions on average.

<img style= "width: 500px; border:3px solid black; margin: 0 auto;" src="http://cgerson.github.io/images/Avg_Rec_pd_Osc.png"/>


## Statistical findings: and the Oscar goes to...

Running an ordinary least squares regression reveals that neither the length of the actor's career nor the age they begin acting has a strong effect on their success. More surprisingly is that the number of months in economic recessions between ages 20-25 has a <b>positive</b>, albeit slight, effect on success. When the going gets tough...? 

However, with an R-squared of only .25, we can confidently conclude that something other than the career length, the gender, the age career begins, and the number of recessions in one's early life is influencing the actor's success. My model as is cannot account for the variability.


## Caveats

This dataset performed well for my purposes. However, accuracy in answering the initial question could be improved with the following:

* Expand sample to include mid-level actors
* Find salary information for actors, over time
* Use continuous economic indicators to capture intensity of recession
* Remove deseased actors from actors list (there are a few)


## Final presentation

Here is the power point version presented to the <a href="http://cgerson.github.io/thanks/" target="_blank">Mothers of Aspiring Millennial Actors</a>. They were pleased. 

<iframe src="//slides.com/claireger/deck/embed" width="576" height="420" scrolling="no" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>