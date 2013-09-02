---
layout: post
title: "Data Scrapping 101"
tagline: "Yet Another CBSE Marks Data Scraper"
modified: 2013-06-12 
category: tech
tags: [data-scrapping,CBSE,marks,tutorial,python,beautiful-soup]
---
If you did follow [Quora](http://quora.com) or any other news site, you would have noticed [this post](https://deedy.quora.com/Hacking-into-the-Indian-Education-System) by [Debarghya Das](http://www.quora.com/Debarghya-Das), where he used data scrapping to get the ICSE marks and do an analysis on. I just thought it would be a good thing to practice building a data scrapper on, and have managed to build one today, thanks to the request by a friend. 

I am still looking for how to reduce the 4 Million roll numbers possible to the ~1 Million who wrote the CBSE Examination. 

The output is a CSV as follows.

* Roll Number
* Name Initials
* Father's Name Initials
* Mother's Name Initials
* Subject Code 1
* Marks 1
* Subject Code 2
* Marks 2
* ...

The code is here 

{% gist 5759693 scrapper.py %}

__Important Note : I do NOT have the permission to run this script for more than usual limits, so if you want to do the analysis you would have to run it on your own__