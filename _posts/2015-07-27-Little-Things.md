---
layout: post
title: Little Things
---

Python's <a href="https://pyformat.info/" target="_blank">formatting method</a> is my favorite code discovery of the week. And it's only Monday.

The formatter responds to replacement fields surrounded by curly braces. Pass arguments to be replaced and ta-da, beauty. 

You can even define your own formatting object. Here's an example that's 

    class DeepThought(object):
    	  def __format__(self, format):
	      if (format == 'answer-to-ultimate-question'):
	      	 return "42."
	      return "What's the question?"
    print '{:answer-to-ultimate-question}'.format(DeepThought())

42.

In sum,

    num = 100.033452
    adj = "real"
    print "Things just got {0}. And {1:0.0f} times prettier.".format(adj,num)

Things just got real. And 100 times prettier.

