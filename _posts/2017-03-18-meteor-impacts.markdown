---
layout: post
title: All known meteor impacts on Earth
excerpt: A map of impact structures on planet Earth
tags: space maps meteors carto
date: 2017-03-18
---

![figure](/assets/img/meteors/crater-grid.png)

If you've ever had the opportunity to peer at the moon through a telescope you've probably noticed how featured it is. Its surface is pock-marked with numerable craters, and depending on its phase the sun can cast striking shadows. This was something Galileo noticed when he first pointed his telescope at the moon, and it was these observations that revealed the moon as imperfect. This upended the notion of perfect heavenly spheres and contributed to the acceptance of Copernicus' theory that Earth itself was an imperfect celestial body.

Earth, of course, **is** a celestial body, just like the moon, and there is evidence of this all around us. Our planet has been and continues to be hit by debris from space, some of which leave lasting impressions.

<iframe width="100%" height="520" frameborder="0" src="https://dcarmody.carto.com/viz/ee204238-ade5-11e6-9558-0e05a8b3e3d7/embed_map" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

This map shows [**impact structures**](http://www.impact-structures.com/) here on Earth. Impact structures are craters or the remnants of craters left by a meteor impact, and they show evidence of the constant bombardment our planet is under. The red dots show the location of an impact structure, while the orange circles show the estimated radius.

Since some of these impacts occurred millions of years ago not all have visible craters. Instead, evidence of an impact is often built based on geological evidence like anomalous amounts of fused glass and shocked minerals.

As I made this map I poked around at a few structures. Here are some of my favorites:

   -   **Meteor, Arizona** - This is the only impact structure that I've visited. This land is privately owned and operated as a tourist attraction. The price for admission is a bit steep, but the crater itself is the best preserved on Earth, a remnant of an impact only 50,000 years ago.
![figure](/assets/img/meteors/meteor_arizona.jpeg)

   -   **Manicougan** - Over 200 million years old, this structure is now visible as a ring lake in Quebec, Canada.
![figure](/assets/img/meteors/ring_lake_canada.jpeg)

   -   **Chicxulub** - The dinosaur killer. Although there's not much to see anymore, this structure is what's left of a massive impact about 65 million years ago.
![figure](/assets/img/meteors/chicxulub.jpeg)

There are others, as well. Check out someone else's [list of favorites](http://www.wondermondo.com/Best/World/ImpressiveImpactCraters.htm). (These are the ones that make up the collaged picture above.)

A lot of factors go into determining just how big of a crater any given meteor might make. There are a few online simulators that allow you to repeatedly smash space rocks into out planet: [ImpactEarth](http://www.purdue.edu/impactearth/) and the [Impact Calculator](http://simulator.down2earth.eu/planet.html).

The Earth is an interesting place for many, many reasons. It is socially diverse and geologically complex, and there is admittedly much that requires our attention. Nevertheless, reminding ourselves that Earth itself is part of a larger context can bring an illuminating shift in perspective. These craters are everywhere. Visit and explore!

Post-script for data-minded folks
---------------------------------

There are a few sources of the data used to make this map. There is a detailed dataset available for [download][data-download]. I found the locations of this data to be slightly off from the visible locations in satellite imagery, so instead I used data scraped from [this table][somerikko].

The trickiest part of making the map was going from lat/lon positions and diameters to circles that accurately represented the structure size. The basic map markers within CARTO scale as you zoom in or out. It's easy to create markers that are *proportional* to the structure diameter, and these can be useful for seeing the relative size of the various structures. But I wanted to see the *exact* size, and I wanted this to stay fixed as you zoom. Of course, for all things technical [StackExchange has the answer](http://gis.stackexchange.com/questions/81520/i-want-to-add-a-circle-which-stays-the-same-size).


[somerikko]: http://www.somerikko.net/impacts/database.php

[searchable-database]: http://tsun.sscc.ru/nh/impact.php

[data-download]: http://impacts.rajmon.cz/IDdata.html
