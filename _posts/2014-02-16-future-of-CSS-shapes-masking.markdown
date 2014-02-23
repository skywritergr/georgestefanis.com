---
layout: post
title:  "The future of CSS. CSS Shapes and CSS Masking."
date:   2014-02-23
categories: blog
---

Last week i went to a [Meetup](http://www.meetup.com/londonweb/) and watched a great talk by [Razvan Caliman](http://razvancaliman.com/) named [The Expressive Web](http://razvancaliman.com/londonweb-2014/#/) where he talked about several upcoming CSS features. Some of them are already partially supported by modern browsers (no IE8, you are not modern) and some of them are not but are still cool features. Browsers like [Chrome Canary](https://www.google.co.uk/intl/en/chrome/browser/canary.html) or [Webkit Nightly](http://nightly.webkit.org/) support most of these features, so you can play with them there. From all the things he talked CSS Shapes and CSS Masking got my attention.

CSS Shapes and Masking are features that, if all browsers had support for them, you could use right away in your project. For example taking a square picture and making it circular for a login button in your navigation bar can now been done via CSS without post process or any library/JS/Whatever. Also you can float text beautifully around a picture of any element with CSS Shapes, and the entire presentation of your web page goes to another level. Below I'm giving some examples how I used these features for my own website.

##Some prerequisites
First things first, in order to see the end result in your browser you need to enable the experimental web on Chrome Canary.

* Copy and paste chrome://flags/#enable-experimental-web-platform-features into the address bar, then press enter.
* Click the 'Enable' link within that section.
* Click the 'Relaunch Now' button at the bottom of the browser window.

Once you done that check [my original about page](http://georgestefanis.com/about/) and then check how it looks using [CSS Shapes and Masking](http://georgestefanis.com/experiments/funky-me.html). In case you haven't install canary, this is how the about looks after applying the new CSS.

![About Me]({{ site.url }}/assets/new-about.png)

The important bit here is how the same amount of information is being presented aesthetically better, using less space. Also note that this is an experiment, the page can look 100 times better. Here is an example of adobe using the same features to present [Alice in Wonderland](http://adobe-webplatform.github.io/Demo-for-Alice-s-Adventures-in-Wonderland/). Amazing huh?

##CSS Masking
So initially i wanted to make my picture circular, because this is the latest trend on the web. That was pretty simple to be honest, i used the following CSS on my IMG tag.

{% highlight css %}
img {
	float: left;
	margin: 5px;
	-webkit-clip-path: circle(140,120,120);
}
{% endhighlight %}

Note here that just doing clip-path won't work (or at least didn't work for me). Applying the above made my picture circular, floating left and with a margin of 5 pixels. All jolly good fun. You can also use any other shape you want. You can read more about clipping and masking in [this article](http://www.html5rocks.com/en/tutorials/masking/adobe/).

##CSS Shapes
Now that i made my picture circular, i wanted the text to float around it beautifully and shapes was my friend. There are two features that i used, shape-inside and shape-outside, and yes you can use them both for the same element. **shape-outside** is the feature that dictates to the browser how the text should float around the element. So by applying shape-outside: circle(134px at 50% 50%); on my IMG tag i told the browser to wrap the text around it and treat it like a circle (and not like a square that the image actually is). After applying that the IMG CSS looked like that:

{% highlight css %}
img {
	float: left;
	margin: 5px;
	-webkit-clip-path: circle(140,120,120);
	shape-outside: circle(134px at 50% 50%);
}
{% endhighlight %}

Now the last bit was to make the text, that had the social media, circular too (i like circles) and float it to the right side of the main text. That proved to be trickier than i thought, but thanks to [Razvan](https://twitter.com/razvancaliman) that [helped me](http://codepen.io/oslego/pen/wmtap) on Twitter i solved it.

My DOM initially was like that, and it didn't work:

{% highlight html %}
<div id="mainText">
.....
</div>
<div id="social">
.....
</div>
{% endhighlight %}

My CSS:

{% highlight css %}
#mainText {
	width: 900px;
	margin: 0 auto;
	text-align: justify;
}

#social {
	shape-inside: circle(143px);
	width: 300px;
	height: 500px;
	text-align: justify;
	float: right;
	shape-outside: circle(150px at 50% 50%);
}
{% endhighlight %}

Changing the DOM though did the trick. I ended up moving the social Div inside the main text div and that did the trick, it worked!!

{% highlight html %}
<div id="mainText">
	<div id="social">
	....
	</div>
	....
</div>
{% endhighlight %}

Razvan further explains the mistaked i made in codepen.io demo i posted above. 

###Making the text div circular
Using the shape-inside feature you are dictating the browser to wrap the contents of the element as a specific shape. As with shape-outside, you can use any shape you fancy.

{% highlight css %}
	shape-inside: circle(143px);
{% endhighlight %}

[More about shapes here](http://codepen.io/collection/qFesk/).

###Setting the shape-outside
The final thing was to make the text wrap the newly created circular div correctly. That was now easy, since we did it before with the image. So using shape-outside again does the trick again.

{% highlight css %}
	shape-outside: circle(150px at 50% 50%);
{% endhighlight %}

And that's it. Now everything works as i wanted to work and looks great. All these things are of course experimental but the image clipping works just fine on Chrome and on Safari. I will be using it for my project on the user login dropdown. So on Chrome and Safari the user image will be circular and on unsupported browsers it will look like a square (which isn't the end of the world). In the near future though all new browsers will support it. That way you can spend zero resources in image processing and instead spend them elsewhere.

You can read more about new (or existing) CSS feature over to [w3.org](http://www.w3.org/Style/CSS/specs.en.html)