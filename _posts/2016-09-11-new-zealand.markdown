---
layout: post
title: A New Zealand Cycle Tour
excerpt: A two week bike tour around the south island.
tags: mapbox projects travel newzealand biking maps photos
image: /projects/images/nz-preview.png
project: true
---


[![image](/projects/images/nz-preview.png)](/newzealand)

**click on image for interactive map**

A couple of years ago my friend Jake, returning from a month at the south pole research station, was in New Zealand for a few weeks and looking for someone else to join him in some adventuring. I couldn't pass up such a wonderful opportunity, so I bought a plane ticket, researched some logistics (yes, in that order), and he and I spent almost two weeks bike touring around the south island.

I took a bunch of photos while down there, both with my own Canon DSLR as well as a borrowed GoPro. For a while these photos sat in a [Flickr photo album][flickr], but I wanted to do something more with them, something that presented what we had done in an interactive web format. I love maps, and the wandering, geographic nature of this trip suggested that a map based navigation was the best way forward. I found a nice [blog post][hahn] by Young Hahn that used Mapbox to plot out a Sherlock Holmes story, and with a few tweaks I was able to use that format for the bike tour. My adapted code is up on [Github][github].

There were a few additional things I would have liked to add to the map, such as markers for the overnight spots and a line representing the route itself, but I moved on to other things before sorting out those issues. At some point you have to label a project good enough and move on. All in all, though, I'm still pretty happy with it.

![image](https://farm8.staticflickr.com/7294/12384549513_9643830484_z_d.jpg)

**Tools:**

Photos were taken with either a digital Canon Rebel with 50mm lens, or a GoPro. Mapping was done with HTML, JavaScript, and the Mapbox API. 


[flickr]: https://www.flickr.com/photos/carmodydr/albums/72157640553163783/with/12385807014/
[hahn]: http://alistapart.com/article/hack-your-maps
[github]: https://github.com/carmodydr/carmodydr.github.io/tree/master/newzealand
