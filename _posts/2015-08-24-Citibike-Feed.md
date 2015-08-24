---
layout: post
title: Citbike Feed
---

Some facts about me:

 * I'm subletting in Brooklyn for the summer
 * I work all day in the Flatiron District
 * I love biking
 * Riding the subway irritates me

Ergo, I might be a perfect candidate for the Citibike bike share program.

Yes, Citibike membership is an option. But I didn't want to commit until I had <b>proof that a bike would be available to me at the specific times I would need one</b>.

So, I wrote a simple script to read Citibike's <a href = "https://www.citibikenyc.com/stations/json" target="_blank">system feed data</a> to understand the bike availability at specified stations. It will store selected data into a dictionary, then write the selected data into a csv file called "citibikedata.csv".

Note: This script is written to work in conjunction with crontabs, to load system data automatically at specified times. That code will be copied below the python script.

<i>Make it your own: Modify the "my_stations" variable to include any stations you are interested in tracking.</i>

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

Now, this feed grabs data at the current time. But I would need the bike sometime around 8am, every weekday. Let's set up a cronjob to run this script every 3 minutes from 7am to 9am.

On my remote server (where my citibikefeed.py file lives), I opened my crontab on the command line:

```
$ crontab -e
```
And added:

```
  */3 7,8 * * 1-5 python citibikefeed.py
```

This means: run my file every 3 minutes, from 7am to 8:59am, from Mon to Fri.

After one day of running, I graphed my feed in iPython Notebook with seaborn:

```
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

df = pd.read_csv("citibikefeed.csv")
del df['Unnamed: 0']

g = sns.factorplot(x="time", y="bikes", hue="name", data=df,aspect = 2,size=6)
g.set_xticklabels(rotation=90)
g.set(title="Available bikes at selected stations")
```

<img style= "width: 700px;" src="http://cgerson.github.io/images/availbikes.png">