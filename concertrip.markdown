---
layout: post
title: Concertrip: Compose your perfect road trip.
excerpt: Providing personalized musical roadtrips using data.
date:
tags: insight data-science data concertrip web
---

# Summary

Concertrip.me was the site I build as a Data Science fellow with the Insight program.

# Site

My goal for this site was a simple set of pages where users could enter some details about their trip (start location and date, end location and date, musical preference) and then see their suggested itinerary in an intuitively understandable way. There are several pieces that must click together in order for this to work: the framework, the data, the algorithm, and the hosting.

## Flask web framework

Flask is a micro-framework written in Python. Simpler and more lightweight than Django, it provides 

- views
- templates

## Data collection


- spotify API
- scraping with beautiful soup

Events
- bandsintown API

## Algorithm

The algorithm is the most interesting part of the site, from my perspective, and the heart of its functionality.

- selecting top event
- finding shortest path
- edge weighting

## Hosting on AWS

My only goal was to see the site up on the web, so I went for pretty basic hosting. Amazon offers a free tier

- gunicorn

# Conclusion

The site still has issues, the primary problem being that it is just far too slow. There are two related reasons for this, both related to the underlying algorithm. The first reason has to do with the algorithm itself. Finding the shortest path is not a fast process, and doing this for all the events being pulled expounds this problem. Secondly, the number of API calls being also contributes to the lag in returning results to the user.

As a whole, this site is more interesting and novel than functional. It never seemed worthwhile to fix it up more completely, so I've moved on to other things. It's greatest use was for me to learn all the various pieces that made it possible.

[hyptertext]: link
