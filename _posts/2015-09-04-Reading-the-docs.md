---
layout: post
title: Reading the docs
---

####What I'm doing:
Reformatting dates ranging from early 1900's until now, using Python's datetime.strptime method. Straightforward.

####What I saw upon inspection:
I find that I've lost all dates before 1969. Noooo!

####What I thought happened:
Maybe all dates before 1969 were formatted in a way I hadn't expected... no, they were the same... maybe all observations dated before 1969 didn't comply with another part of my cleaning stage... no, they were real similar to all the others...

####What actually happened:
Python's datetime.strptime method added a century to every date before 1969. In other words, 1/1/68 became reformatted as 1/1/2068. In a later processing stage, I had removed all dates from the future, because my data is historical and future observations were impossible.

####What the <a href="https://docs.python.org/2/library/time.html" target="_blank">docs</a> say:
"When 2-digit years are accepted, they are converted according to the POSIX or X/Open standard: values 69-99 are mapped to 1969-1999, and values 0–68 are mapped to 2000–2068."

####Takeaway:
Sometimes (always) it's a good idea to reference the documentation of modules when code isn't behaving as expected.

####Also:
Dates are a pain.

