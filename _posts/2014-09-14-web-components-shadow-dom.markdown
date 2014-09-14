---
layout: post
title:  "Web Components: What is shadow DOM and how to use it."
date:   2014-09-14
categories: blog
---

[Web Components](http://www.w3.org/TR/components-intro/) is a new specification that is a set of four other specifications: 

1. [Templates](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/templates/index.html)
2. [Shadow DOM](http://www.w3.org/TR/shadow-dom/)
3. [Custom Elements](http://w3c.github.io/webcomponents/spec/custom/) and
4. [Packaging](http://w3c.github.io/webcomponents/explainer/).

Here we'll be talking for Shadow DOM as it's one of the most intriguing concepts, and it's also something that you can use even today in your projects. To understand what web components are and how useful they are, you have to think about C or Java. In C, for example, if you go ahead and write your entire code inside the main function the result will be an awful mess of spaghetti code that none will be able to read. In HTML on the other hand such a concept doesn't exist, there is no way to encapsulate and break down your HTML code in smaller pieces (widgets). That's what Web Components and Shadow DOM are here for.

Think of your home.html as your main function. Ideally in there instead of having the entire HTML code, you would like to have calls to individual widgets that when you connect them together they create your final result; kinda like Lego. That makes your code more readable, easier to work on and more importantly it helps encapsulate it. Shadow DOM is the the part that does the encapsulation.

##Shadow DOM vs the DOM
Shadow Dom is the ability of the browser to include a subtree of DOM elements into the rendering of a document but not inside the main DOM. So in brief, the DOM is the elements you see rendered on your browser (and are part of the main DOM) and shadow DOM are elements that are not rendered but are part of the document. The image below hopefully adds some clarity to the differences between the document and the main DOM.

![Document vs Main DOM]({{site.url}}/assets/document-vs-mainDOM.jpg)

So essentially what we're saying is that what you see on your browser is not the only elements your browser has, it keeps some of them secret. Examples of that are HTML elements that are currently used everywhere, like the date selector or the slider or the video component or anything else that HTML offers to you ready to use. If you didn't write the extra elements that come with your tag then there are stored in some shadow DOM root somewhere in the document.
{% highlight html %}
<input type="date" id="someDate">
<input type="range" id="someRange">
{% endhighlight %}
<break>

##How to use it
Now that you have a basic understanding of what shadow DOM is roughly lets start doing something with it. What we're going to do is a login page widget. Normally to create a login widget you would do something like that:

{% highlight html %}
<h3>Welcome to georgestefanis.com. Please Login.</h3>
<label for="username">Username:</label>
<input type="text" id="username">
<br>
<label for="password">Password:</label>
<input type="password" id="password">
{% endhighlight %}
and the result would be: <br>
<h3>Welcome to georgestefanis.com. Please Login.</h3>
<label for="username">Username:</label>
<input type="text" id="username">
<br>
<label for="password">Password:</label>
<input type="password" id="password"><br>

Now that's all nice and good but if i wanted to style specific elements (like the h3 heading) i would have to do some CSS hacks. Also semantically speaking i don't need all that DOM. All i really need is inform my document that this is a login widget for the site georgestefanis.com. So something like that would be better:
{% highlight html %}
<div id="loginForm">georgestefanis.com</div>
{% endhighlight %}

The above code though will not render the same result as our form, it will only print on screen the string "georgestefanis.com". This isn't what we want, we want the entire form.

{% highlight html %}
<div id="loginForm">georgestefanis.com</div>

<template id="loginFormTemplate">
	<h3>Welcome to georgestefanis.com. Please Login.</h3>
	<label for="username">Username:</label>
	<input type="text" id="username">
	<br>
	<label for="password">Password:</label>
	<input type="password" id="password">
</template>

<script>
	var shadow = document.querySelector('#loginForm').createShadowRoot();
	var template = document.querySelector('#loginFormTemplate');
	var clone = document.importNode(template.content, true);
	shadow.appendChild(clone);
</script>
{% endhighlight %}

The above code will give us the result we want (feel free to inspect the form below to see the shadow root etc).
<div id="myloginForm">georgestefanis.com</div>

<template id="myloginFormTemplate">
	<h3>Welcome to georgestefanis.com. Please Login.</h3>
	<label for="username">Username:</label>
	<input type="text" id="username">
	<br>
	<label for="password">Password:</label>
	<input type="password" id="password">
</template>

<script>
	var shadow = document.querySelector('#myloginForm').createShadowRoot();
	var template = document.querySelector('#myloginFormTemplate');
	var clone = document.importNode(template.content, true);
	shadow.appendChild(clone);
</script>

Let's explain the code a little bit. The template tag is like a box where inside it we put our DOM elements and any style we might want to add. You can think of it as a function in C. In there we've added the login form that we create before. Below the template we now create a shadow root, that will host our shadow DOM, on the div and then we append the template to it. That works as before but if I now want to change the site name i need to go and change it in two places, and that's inconvenient and dangerous. So we'll change our code slightly.

{% highlight html %}
<div id="loginForm">georgestefanis.com</div>

<template id="loginFormTemplate">
	<h3>Welcome to <content></content>. Please Login.</h3>
	<label for="username">Username:</label>
	<input type="text" id="username">
	<br>
	<label for="password">Password:</label>
	<input type="password" id="password">
</template>

<script>
	var shadow = document.querySelector('#loginForm').createShadowRoot();
	var template = document.querySelector('#loginFormTemplate');
	var clone = document.importNode(template.content, true);
	shadow.appendChild(clone);
</script>
{% endhighlight %}

The only change we did was inside the h3 tag. In there instead of hard coding the name of the site we added the content tag. What that will do is to append the content of root host (in our case the content of our div) in its place. Therefore if in our div we change the name, that change will reflect in our shadow DOM as well. Now that we've done all that we're ready to individually style our login form without effecting the rest of the website.

{% highlight html %}
<div id="loginForm">georgestefanis.com</div>

<template id="loginFormTemplate">
	<style>
		h3 {
			font-size: 18px;
			font-weight: lighter;
			color: red;
		}
	</style>

	<h3>Welcome to <content></content>. Please Login.</h3>
	<label for="username">Username:</label>
	<input type="text" id="username">
	<br>
	<label for="password">Password:</label>
	<input type="password" id="password">
</template>

<script>
	var shadow = document.querySelector('#loginForm').createShadowRoot();
	var template = document.querySelector('#loginFormTemplate');
	var clone = document.importNode(template.content, true);
	shadow.appendChild(clone);
</script>
{% endhighlight %}

So we've styled our H3 heading to be red, font size 18 pixels and its weight to be lighter. That styling will only effect our login form and nothing else (that page has more than one H3). You should see my page rendered as normal, without any red headings, but the login below should have a red heading (how fancy!).

<div id="loginForm">georgestefanis.com</div>

<template id="loginFormTemplate">
	<h3>Welcome to <content></content>. Please Login.</h3>
	<label for="username">Username:</label>
	<input type="text" id="username">
	<br>
	<label for="password">Password:</label>
	<input type="password" id="password">
</template>

<script>
	var shadow = document.querySelector('#loginForm').createShadowRoot();
	var template = document.querySelector('#loginFormTemplate');
	shadow.innerHTML = '<style>' +
		'h3 {' +
			'font-size: 18px;'+
			'font-weight: lighter;'+
			'color: red;' +
		'} </style>';
	var clone = document.importNode(template.content, true);
	shadow.appendChild(clone);
</script>

##Final thoughts
You should now have a basic idea of how Shadow DOM can be used to create widgets and encapsulation in general. I hope that you are a bit more excited and you can start using it to your projects. You can read more to the following links

* [HTML Rocks, Shadow DOM 101](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/)
* [HTML Rocks, Shadow DOM 201, styling](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/)
* [HTML Rocks, Shadow DOM 301, advanced concepts](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-301/)
* [What the Heck is Shadow DOM?](http://glazkov.com/2011/01/14/what-the-heck-is-shadow-dom/)
* [Web Components by Todd Motto](http://toddmotto.com/web-components-concepts-shadow-dom-imports-templates-custom-elements/)

Also be sure to check out [Polymer](http://www.polymer-project.org/) which is a Google made framework that implements (and more) web components.