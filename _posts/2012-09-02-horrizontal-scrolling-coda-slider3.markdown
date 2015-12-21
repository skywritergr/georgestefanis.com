---
layout: post
title:  "Horizontal Scrolling, Coda Slider 3 and image maps"
date:   2012-09-01
categories: blog
---
Lately I’ve been designing a web site, for a client, that needs to be horizontal scrolling. For those of you who are not familiar, a horizontal web site is one that has all the pages embedded in one, huge, HTML file, separated by DIVs. The scrolling is occurring either by using some JQuery functions of using some library already doing that. We used Coda Slider 3. That site was a bit demanding regarding the design. More specifically the client had specific requirements regarding the position of elements in the page, therefor we went for the option to use an image with the position of elements in the page and use image maps over the image. The problem is though that the image map was “floating” over the page, and since he had one html for all pages and several image maps we were having problems. The maps were not working.

Below I’m attaching the code for the map we had created initially.

{% highlight html limenos %}
<img src="images/word.png" border="0" />
<map name="Map2" id="Map2">
<area shape="rect" coords="107,64,113,72" href="i.html" />
<area shape="rect" coords="219,42,312,53" href="memory_of_water.html" />
<area shape="rect" coords="396,11,519,20" href="waving.html" />
<area shape="rect" coords="304,95,430,101" href="a_woman.html" />
<area shape="rect" coords="473,73,611,80" href="distant_notes.html" />
<area shape="rect" coords="611,44,698,51" href="piece_of_paper.html" />
<area shape="rect" coords="720,101,743,111" href="ebb.html" />
<area shape="rect" coords="66,255,99,263" href="stasis.html" />
<area shape="rect" coords="192,193,244,203" href="unknown.html" />
<area shape="rect" coords="143,118,212,126" href="empty_hotel.html" />
<area shape="rect" coords="687,6,723,17" href="sound.html" />
<area shape="rect" coords="85,173,130,185" href="sea.html" />
</map>
{% endhighlight %}
In terms of coding that piece of code is perfectly fine. It works perfect in a normal standalone web page, but it doesn’t in a horizontal scrolling web site. So how we solved the problem? We used DIVs and CSS to replicate the same thing. Below I’m attaching the code and I shall explain.
{% highlight html limenos %}
<a href="i.html"><div id="pos1"></div></a>
<a href="memory_of_water.html"><div id="pos2"></div></a>
<a href="waving.html"><div id="pos3"></div></a>
<a href="a_woman.html"><div id="pos4"></div></a>
<a href="distant_notes.html"><div id="pos5"></div></a>
<a href="piece_of_paper.html"><div id="pos6"></div></a>
<a href="ebb.html"><div id="pos7"></div></a>
<a href="stasis.html"><div id="pos8"></div></a>
<a href="unknown.html"><div id="pos9"></div></a>
<a href="empty_hotel.html"><div id="pos10"></div></a>
<a href="sound.html"><div id="pos11"></div></a>
<a href="sea.html"><div id="pos12"></div></a>
{% endhighlight %}
CSS:
{% highlight css limenos %}
#pos1{
position:absolute;
width:6px;
height:8px;
top:64px;
left:107px;
}
 
#pos2{
position:absolute;
width:93px;
height:11px;
top:42px;
left:219px;
}

...
{% endhighlight %}
So what we did in the HTML, was create a regular link and inside that link create a DIV. Pretty basic stuff. Then we need to place the div somewhere in the page. We need two things to do that; first, let the CSS know that the DIV position is absolute (therefor won’t move around as the page gets smaller or bigger in different browsers) and finally give it the coordinates. We don’t have the luxury of giving 4 coord numbers to CSS so we play around to replicate that. First we give the position of the DIV from the top, e.g. 64px from the top. Then we give the position from the left, e.g. 107px. Now we miss two more coords to complete our rectangle, right and bottom.

If you look in our first HTML code example, to replicate the exact same rectangle we need the following coordinates coords="107,64,113,72". We have already given above 107px as left and 64px as top; we miss 113px as right and 72px as bottom. So in order to do that we do a little basic math and instead of giving those numbers as coordinates we manipulate how big the DIV will be. So the following formulas apply:

Right coord (width) = 113px – 107px = 6px
Bottom coord (height) = 72px – 64px = 8px

And there we go, it works fine and it doesn’t create any problems. Arguably the HTML image map is much more clean method rather than that, but there are cases where you can’t use an image map. That is a good alternative.