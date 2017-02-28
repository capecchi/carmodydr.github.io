---
layout: post
title: Concertrip: Compose your perfect road trip.
excerpt: Providing personalized musical roadtrips using data.
date:
tags: insight data-science data concertrip web
---

# Summary

Concertrip.me was the site I built as a Data Science fellow with the Insight program. It takes user-entered information about an upcoming roadtrip, combines it with musician and concert data, and outputs a suggested roadtrip itinerary that attempts to see as many relevant live music events as possible. It was built up over the course of about four weeks using a number of technologies, including Flask, MySql, and Mapbox.

# Site

My goal for this site was a simple set of pages where users could enter some details about their trip (start location and date, end location and date, musical preference) and then see their suggested itinerary in an intuitively understandable way. There are several pieces that must click together in order for this to work: the framework, the data, the algorithm, and the display.

## Flask web framework

Flask is a micro-framework written in Python. Simpler and more lightweight than Django, it provides the means by which actions and visualization on the front-end are tied to code and data on the backend. This is accomplished through **views** and **templates**.

- views
- templates

    sample view code


## Data collection

Nothing can happen without data, and Concertrip makes use of several different sources to work its magic. On the front-end there are web forms that collect information from the user, and these are passed by Flask into the back-end Python processing.

I'll talk more about the actual algorithm below, but one of the elements that it requires is similarity relationships between musicians. This is a very interesting problem, but also very complicated, and addressing it in a substantial and effective way is its own project. So I outsourced it. It turns out that LastFM, a music appreciation site, has pages for every artist that contain a list of similar artists. Scrape all this and you have a database of one-to-one similarity relationships.

BeautifulSoup seems to be the defacto standard for web-scraping in Python. It has simple syntax, is straightforward to use, and is quite effective.

    example

The urls at LastFM are constructed like `www.lastfm.com/ARTIST_NAME`, so in order to automate the web-scraping I needed a large set of musician/band names to iterate through. This list I grabbed from Billboard.com. Once I had that, I ran through it to pull the first page of similar artists from every musicians homepage. This gets stored as pairwise relationships in a MySQL database.

Being all about live concerts, Concertrip also needs to know what events are happening! Enter Bandsintown.com, which has an API that allows event information to be pulled given a range of dates, a geographic location, and a search radius.


Events
- bandsintown API
- 
- front end

    API call

## Algorithm

The algorithm is the most interesting part of the site, from my perspective, and the heart of its functionality. It is all based in network analysis and relies on the NetworkX Python library.

- artist similarity metric

- selecting top event
- finding shortest path
- edge weighting


## Displaying results

As fancy as everything might be on the back-end, results are worthless if they aren't understood! For something with such important geographic information as a roadtrip, the most intuitive way to understand the website's output is with a map. [I love maps]()! I love maps so much that I had already spent time prior to this project playing around with JavaScript and Mapbox. This allowed me to adapt what I knew and implement some basic mapping relatively quickly (and within the project's deadlines).

The trickiest part was learning how to pass an array of locations through  Flask into the JavaScript template.

- json
- leaflet
- pop-ups

# Conclusion

The site still has issues, the primary problem being that it is just far too slow. There are two reasons for this, both related to the underlying algorithm. The first reason has to do with the algorithm itself. Finding the shortest path is not a fast process, and doing this for all the events being pulled expounds this problem. Secondly, API calls are not fast either, and the number of calls being made also contributes to the lag in returning results to the user.

As a whole, this site is more interesting and novel than functional. It never seemed worthwhile to fix it up more completely, so I've moved on to other things. It's greatest use was for me to learn all the various pieces that made it possible.

[hyptertext]: link
