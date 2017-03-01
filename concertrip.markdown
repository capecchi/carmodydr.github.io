---
layout: post
title: "Concertrip: Compose your perfect road trip."
excerpt: Providing personalized musical roadtrips using data.
date: 02-28-2017
tags: insight data-science data concertrip web
---

# Summary

Concertrip.me was the site I built as a Data Science fellow with the Insight program. It takes user-entered information about an upcoming roadtrip, combines it with musician and concert data, and outputs a suggested roadtrip itinerary that attempts to see as many relevant live music events as possible. It was built up over the course of about four weeks using a number of technologies, including Flask, MySql, and Mapbox.

# Site

My goal for this site was a simple set of pages where users could enter some details about their trip (start location and date, end location and date, musical preference) and then see their suggested itinerary in an intuitively understandable way. There are several pieces that must click together in order for this to work: the framework, the data, the algorithm, and the display.

## Flask web framework

Flask is a micro-framework written in Python. Simpler and more lightweight than Django, it provides the means by which actions and visualization on the front-end are tied to code and data on the backend. This is accomplished through **views** and **templates**.

A view allows you to determine what happens when a user visits a particular url, potentially collecting information and chucking into some Python code before rendering it in a template.


```
    def multiplyItByTen(number):
        return number*10

    @app.route('/')
    @app.route('/index')
    def roadtrip_input():
        foo = request.args.get('user_entered_variable')
        bar = multiplyIt(foo)
        return render_template("index.html", var1 = foo, var2 = bar )
```

Variables passed within `render_template` can be accessed using Jinga bracket notation. These brackets can be used anywhere in the template, including the HTML tags and JavaScript code (as I'll demonstrate later).

```
    <p>You've passed the variable {{ foo }}, but we multiplied it and now it's {{ var2 }}!</p>
```

## Data collection

Nothing can happen without data, and Concertrip makes use of several different sources to work its magic. On the front-end there are web forms that collect information from the user, and these are passed by Flask into the back-end Python processing.

I'll talk more about the actual algorithm below, but one of the elements that it requires is similarity relationships between musicians. This is a very interesting problem, but also very complicated, and addressing it in a substantial and effective way is its own project. So I outsourced it. It turns out that LastFM, a music appreciation site, has pages for every artist that contain a list of similar artists. Scrape all this and you have a database of one-to-one similarity relationships.

BeautifulSoup seems to be the defacto standard for web-scraping in Python. It has simple syntax, is straightforward to use, and is quite effective.

    EXAMPLE OF BS4

The urls at LastFM are constructed like `www.lastfm.com/ARTIST_NAME`, so in order to automate the web-scraping I needed a large set of musician/band names to iterate through. This list I grabbed from Billboard.com. Once I had that, I ran through it to pull the first page of similar artists from every musician's homepage. This gets stored as pairwise relationships in a MySQL database.

Being all about live concerts, Concertrip also needs to know what events are happening! For this I turned to Bandsintown.com, which has an API that allows event information to be pulled given a range of dates, a geographic location, and a search radius.

## Algorithm

The algorithm is the most interesting part of the site, from my perspective, and the heart of its functionality. It is all based in network analysis and relies on the NetworkX Python library.

### Artist similarity metric

In order to know what events best match the musical preferences of the user I needed some way to assess the 'goodness' of a band or musician. I decided to do this by asking the user for the name of an artist they like and then evaluating the similarity between that artist and those that are playing live concerts.

Initially I was thinking of using the Spotify API to calculate distance in a high-dimensional feature space, but the API only has information for songs, not artists, and I decided that putting together something effective would take more time than I had.

As I mentioned above, I outsourced the problem and scraped data from LastFM, generating a large list (~80,000 entries) of pairwise relationships. Using this I constructed a *similarity network*, in which you can hop from artist to artist. The **similarity metric** I use is just the shortest path between two musicians in this network.

### Route finding

Judging "musical fit" is only one necessary ingredient - I also have to construct the roadtrip itself! There are a few steps to this algorithm.

#### Form a search grid from start to end.

#### Pull events in each grid location, rank them using the similarity metric, keep only the top one.

#### Construct a network of these top ranking events.

directed graph, forward in time, not too far

#### Weight edges based on distance and similarity and find the shortest path.


IMAGES


## Displaying results

As fancy as everything might be on the back-end, results are worthless if they aren't understood! For something with such important geographic information as a roadtrip, the most intuitive way to understand the website's output is with a map. [I love maps!](http://www.danielcarmody.net/projects) I love maps so much that I had already spent time prior to this project playing around with JavaScript and Mapbox. This allowed me to adapt what I knew and implement some basic mapping relatively quickly (and within the project's deadlines).

The trickiest part was learning how to pass an array of locations through  Flask into the JavaScript template. The event information is created as a number of different arrays in Python and then passed to the map template.


```
    return render_template("map.html", placesList = placesList, eventList = topEvents, startName = start, endName = end)
```

These arrays are iterated over to place Leaflet markers on the map and populate the pop-up tooltips.


```
	for (i=0; i < {{ placesList }}.length; i++) {
		var locLat =  {{placesList}}[i][0];
		var locLon =  {{placesList}}[i][1];
		var tooltip = '<h1>'.concat('Band: ',bandArr[i],'<\/h1><h2>Venue: ',
			venArr[i],'<\/h2><h3>',dateArr[i],'</h3>');
		if (bandArr[i] == 'Start') {
			tooltip = 'Start'; }
		if (bandArr[i] == 'End') {
			tooltip = 'End'; }
		var color = "#3ca0d3"; // blue, color for unchosen event
		if (colorArr[i] == 1) { color = '#ff3333'; }
		L.marker( [locLat,locLon], {title: String(bandArr[i]),
				icon: L.mapbox.marker.icon({
    				    'marker-size': 'large',
    				    'marker-symbol': 'music',
    				    'marker-color': color })
			 } ).addTo(mapLeaflet).bindPopup( tooltip );
	}
```

It might be a bit janky, but it works!

# Conclusion

The site still has issues, the primary problem being that it is just far too slow. There are two reasons for this, both related to the underlying algorithm. The first reason has to do with the algorithm itself. Finding the shortest path is not a fast process, and doing this for all the events being pulled expounds this problem. Secondly, API calls are not fast either, and the number of calls being made also contributes to the lag in returning results to the user.

As a whole, this site is more interesting and novel than functional. It never seemed worthwhile to fix it up more completely, so I've moved on to other things. It's greatest use was for me to learn all the various pieces that made it possible.
