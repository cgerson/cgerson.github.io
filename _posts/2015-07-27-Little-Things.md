---
layout: post
title: Formatting the Little Things
---

Python's <a href="https://pyformat.info/" target="_blank">formatting method</a> is my favorite code discovery of the week. And it's only Monday.

The formatter responds to replacement fields surrounded by curly braces inside a string. Call the "format" method on the string, specifying which values to place inside those curly braces and ta-da, beauty. 

You can even define your own formatting object. Here's an example to help format one of life's most <a href="https://en.wikipedia.org/wiki/List_of_minor_The_Hitchhiker%27s_Guide_to_the_Galaxy_characters#Deep_Thought" target="_blank">difficult questions</a>:

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

