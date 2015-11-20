---
layout: post
title: Maternity Leave by Industry
---

How many weeks of maternity leave do US industries offer their employees?

The website <a href = "https://fairygodboss.com/maternity-leave-resource-center" target="_blank">Fairygodboss</a> hosts a crowdsourced collection of maternity leave information. Each observation may include the name of the company, the industry, and the amount of paid and unpaid leave (in weeks) that the company offers.

This is a great example of important data that is not made public by companies or, if public, is fragmented. With crowdsourcing, individuals from disparate parts of the economy can come together and create a powerful and telling database. Yeehaw!

The code used to scrape and clean the data lives in this <a href = "https://github.com/cgerson/maternity-leave" target="_blank">GitHub repo</a>. The main tools used were BeautifulSoup (to scrape) and pandas (to manipulate the data).

Here's the gist:

```
# generate BeautifulSoup object 
url = "https://fairygodboss.com/maternity-leave-resource-center"
response = requests.post(url)
page = response.text
soup = BeautifulSoup(page,"html.parser")
```

```
# scrape company information
collect_cos = []
for line in soup.findAll('a',attrs = {'class':'comp_page'}):

    #filter out line breaks and remove extra white space
    co = [i.text.strip() for i in line.children if str(i) not in ['\n']] 

    #append company to list
    collect_cos.append(co)
```

```
# create pandas dataframe object
df = pd.DataFrame(collect_cos, columns = ['company','industry','paid','unpaid'])
```

Currently there are <b>805 companies</b> from <b>40 industries</b> (lastest update: Nov 20, 2015).

Average paid leave in weeks over all companies submitted is <b>8.1 weeks</b>. Average unpaid leave is <b>9.3 weeks</b>.

Two outliers in this sample, <b>Bill and Melinda Gates Foundation</b> (Nonprofit) and <b>Netflix</b> (Technology), offer 52 weeks of paid maternity leave. 

The 20 companies with industry "Unspecified" (including Smucker's, Petsmart and Texas Children's Hospital) should be separated into their corresponding industry bucket -- on the to-do list.

Plotting the average leave offered by industry:
<br><br>
<iframe width="750" height="900" frameborder="0" scrolling="no" src="https://plot.ly/~cgerson/48.embed"></iframe>