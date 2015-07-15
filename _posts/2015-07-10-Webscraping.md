---
draft: true
published: false
layout: post
title: Webscraping
---

Webscraping for the win.

This week we are using BeautifulSoup to extract data from websites.

My approach was to extract from pages of the same format from the same root site, finding identifier tags for desired data and creating a formula to locate and extract in the same way for every page.

First road bump: tags vary for the same data.

Example: 
Most names are linked: http://www.boxofficemojo.com/oscar/chart/?view=allcategories&yr=2014&p=.htm
Few names are linked: http://www.boxofficemojo.com/oscar/chart/?yr=2002&view=allcategories&p=.htm

My current approach, then, is to mine manually. Still hopeful of finding a more automated way.

Update: have mined birthdays from Wikipedia for my dataset. Very effective. Only 29 of 728 were not found. Inputting manually. With a smarter system, I could search last name only, and key words. Cleaning birthdays -- converting to datetime object, stripping whitespace.

Writing straight to csv avoids unicode problem, converts to string (or becomes string once loaded back into Python)

Controlling for "principal occupation" by creating dummy variable, where 1 is if "Actor" or "Actress" is the first occupation listd on their Wikipedia page.

Measuring number of months lived through a US recessionary period between certain ages. Assuming US recession affects global economy (re foreign actors), certainly would affect Total Gross of movies

Total Gross variable in millions

Do economic dips determine the success of Hollywood actors?

Success means high grossing films.

Actors are contemporary actors

Films featuring these actors grossed ...

Narrow down dataframe to complete info

Mothers of Aspiring Millenial Actors (MOMA)
- Unfortunately, I cannot give you data on Actors who didn't make it

Probability of earning more given recession given you've "made it"

Some input manually, "The Rock" for example
- as mentioned before, with a better system, if value generated was none, I could go back and Google actor name ("The Rock" in this instance), then find the Wikipedia entry. Or google through Wikipedia directly.
- some Years active had (screen) or (acting) in parenthesis that must have confused scraper...


Variables:
Actor = unique ID
Total_Gross_