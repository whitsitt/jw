---
date: 2018-06-22T01:00:00.000+00:00
author: Joe Whitsitt
cover:
  image: "images/elcarito-CRn-_80z4SE-unsplash.jpg"
  relative: false
title: Optimizing GeoJSON
category: web development
tags:
  - mapping
  - geojson
type: post
comments: false
aliases:
  - /2018/06/22/optimizing-geojson/
  - /blog/optimizing-geojson
  - /posts/optimizing-geojson
---
I have been working with some GeoJSON files lately for work and at first I was having issues with the large size of the files. For the web (displaying it on a map), this is not good so I went in search of some ways to reduce the file size.

## Trim (Truncate) Coordinates

I read that, "[for most web maps, decimals after the 5th decimal point are essentially meaningless,](https://sandbox.idre.ucla.edu/sandbox/general/optimize-geojson)" so using the find and replace functionality in Sublime Text:

**Find:**

{{< highlight diff >}}
([0-9]+\.[0-9]{5})([0-9]+)
{{< / highlight >}}

_The 5 stands for decimal points. Adjust as needed._

**Replace**

{{< highlight diff >}}
\1
{{< / highlight >}}

Also, remove the elevation portion of the coordinates if you don't plan to use it.

## Clean-up Attributes

There were a lot of attributes nested alongside the coordindates that I didn't need, so I removed them. Typically for work and this example in particular, most of the attribute information I need to associate with these features are stored elsewhere. Mainly for accessibility purposes, we try to take users away from the map as soon as possible for more information. We also try to have the map data in an accessible listing for those who can't interact with the map.

I also took at shortening the attribute names that I was keeping. These are reprinted over and over, so the less characters the better.

## Compact/Minify

White space is bad for file size. Though it helps with readability, unless I need to manually correct data, only parsers will be looking at the raw data. There is a cool tool for validating and formatting JSON: [https://jsonformatter.org](https://jsonformatter.org)

In the end using these tips, one file was reduced from 3 MB to 500 KB!
