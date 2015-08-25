---
layout: post
title: Evaluating Citibike as a commuting option
---

Or, how to write code to grab information so you don't have to. 

Here are some facts about me:

 * I'm subletting in Brooklyn for the summer
 * I work all day in the Flatiron District
 * I love biking
 * Riding the subway irritates me

Ergo, I might be a good candidate for the <a href="https://www.citibikenyc.com/" target="_blank">Citibike bike share program.</a> However, I didn't want to commit until I had <b>proof that a bike would be available to me at the specific times I would need one</b>.

So, I wrote a simple python script on my remote server to read Citibike's <a href = "https://www.citibikenyc.com/stations/json" target="_blank">system feed data</a> to understand the bike availability at specified stations. It stores selected data into a dictionary (station name, available bikes, available docks, current time), then writes the selected data into a csv file called "citibikedata.csv".

The key here is to work in conjunction with <a href="http://www.adminschoice.com/crontab-quick-reference" target="_blank">crontabs</a>, which will run my code in the background at specified times. Find that code below the python script.

<i>Make it your own:</i> Modify the ```my_stations``` variable to include any stations you are interested in tracking. Find station names <a href="https://member.citibikenyc.com/map/" target="_blank">here.</a>

#### citibikefeed.py

```
import urllib, json
import pandas as pd
from datetime import datetime
import os.path

url = "https://www.citibikenyc.com/stations/json"
response = urllib.urlopen(url)
data = json.loads(response.read())

my_stations = ["Fulton St & Washington Ave","Fulton St & Grand Ave",
               "Fulton St & Clermont Ave","Lefferts Pl & Franklin Ave"]

d={'name':[],'docks':[],'bikes':[],'time':[]}
for station in data["stationBeanList"]:
    if station["stationName"] in my_stations:
        d['name'].append(str(station["stationName"]))
        d['docks'].append(int(station['availableDocks']))
        d['bikes'].append(int(station['availableBikes']))
        d['time'].append(datetime.strptime(str(data["executionTime"]),"%Y-%m-%d\
 %I:%M:%S %p"))

df = pd.DataFrame(d)
f = "citibikedata.csv"

if os.path.isfile(f)==True:
    df.to_csv(f,mode="a",header=False)
else:
    df.to_csv(f,mode="w",header=True)
```

Now, this feed grabs data at the current time. But I would need the bike sometime around 8am, every weekday. Let's set up a cronjob to run this script between 7am and 9am.

On my remote server (where my citibikefeed.py file lives), I opened my crontab on the command line:

```
$ crontab -e
```
And added:

```
  */3 7,8 * * 1-5 python citibikefeed.py
```

This means: run my file every 3 minutes, from 7am to 8:59am, from Mon to Fri.

After one day of running, I <b>plotted my feed</b> in iPython Notebook with seaborn:

#### citibikegraph.ipynb
```
import pandas as pd
%matplotlib inline
import seaborn as sns

df = pd.read_csv("citibikefeed.csv")

g = sns.factorplot(x="time", y="bikes", hue="name", data=df,aspect = 2,size=6)
g.set_xticklabels(rotation=90)
g.set(title="Available bikes at selected stations")
```

<img style= "width: 780px;" src="http://cgerson.github.io/images/availbikes.png">

Great! Bikes galore.

<i>Next steps:</i> This script can easily be expanded to include dock availability at destination station, as well as available docks at your neighborhood station for the return journey.