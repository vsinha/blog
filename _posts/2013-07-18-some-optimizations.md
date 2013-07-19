---
layout: post
title: "Some Optimizations"
description: ""
category: 
tags: []
---


In what started as a curious experiment, I've made a couple of load speed optimizations to the site. Here's a post about it. 

Because I wanted to have a metric of this process, I started by running a web page load speed test at webpagetest.org. 

<!--more-->

This was my original result:

<img src="/assets/speed/legend.png">
<img src="/assets/speed/1.png">


All this takes 0.847s to have the page fully loaded according to webpagetest, represented by the dark blue "document complete" bar.

Let's break this down:

1. To be expected, simply the index.html.
2. The first font call, for the "Viraj Sinha" at the top of the nav sidebar. Originally it was using a font called Wire One, grabbing it off Google's font api when the index.html loaded.
3. Base CSS
4. This is a script included in Jekyll Bootstrap, which I've realized I don't actually need. This is eating a whopping 358ms.
5. Fetches the CC license image I have in the footer, also takes quite a while evidently
6. Another google font API call
7. Google analytics 
8. Another theme something?
9. More Google analytics


I removed the javascript and swapped the font for a more typographically boring choice which doesn't require an API call. Then I added the CC license image png to the site repository so we don't have to go get it from the creative commons website every time. 

This left me with this:

<img src="/assets/speed/3.png">

All that left me with 0.200s to fully loaded. Not bad at all! Having the CC license image saved 208ms alone - although that request happened simultaneously with the javascript load and a font call, so that one fix alone wouldn't have helped nearly as much. A 0.647s decrease in page load time is pretty appreciable, especially if we take mobile browsing experiences into account.