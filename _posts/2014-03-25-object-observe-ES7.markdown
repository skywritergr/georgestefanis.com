---
layout: post
title:  "Why Object.observe is the best feature of ES7 so far"
date:   2014-03-25
categories: blog
---

For the past year i've been reading a lot about Object.observe and all the magic it will add in our apps. Very recently though i've read that [Chrome will be shipping Object.observe](https://groups.google.com/forum/#!topic/v8-users/aeSFJK1L5n4) soon. I have no idea how soon though since they need to test the performance more, but it's already available in Chrome Canary and you can start playing right now.


##The Basics
The simplest example ever is observing an object for changes in its variables and in its general state.

{% highlight javascript %}
var obj = {};

Object.observe(obj, function(changes){
	changes.forEach(function(change){
		// do stuff with change.
		console.log(change.type, change.name, change.oldValue);
	});
});
{% endhighlight %}

So now if you go to your console you can start playing with your new object.
{% highlight javascript %}
obj.foo = 1 // output: add foo undefined
obj.foo = 5 // output: update foo 1
delete obj.foo // output: delete foo 5
{% endhighlight %}

So you can see that Object.observe notifies us about the old value of our object, the type of the change and the name of the object we're changing. This is extremely neat, and in my opinion gets JavaScript developing to a whole new level. Obviously you can do all sorts of other, more complicated, stuff like creating your own accessor notifiers by using the Object.getNotifier function. An excellent mini tutorial on how to do that can be found [here](http://weblog.bocoup.com/javascript-object-observe/). Also, the always amazing Addy Osmani [talked about Object.observe](http://addyosmani.com/blog/the-future-of-data-binding-is-object-observe/) last year at JSConfEU and i really urge you to watch that video.

##What next?
The next step for you is to go away on Chrome Canary and start playing with Object.observe. It's extremely obvious that Object.observe is very easy to grasp, as a concept, and value its use. Also you can read [this post](http://amasad.me/2014/03/16/why-im-excited-about-objectobserve) by Amjad Masad and [the harmony wiki](http://wiki.ecmascript.org/doku.php?id=harmony:observe) on Object.observe. 

While you do that, the browser vendors need to implement and test the overall performance of the Object.observe. So far only Chrome supports it, but i hope Firefox and Webkit will catch up soon. In fact Firefox has already [a Bugzilla issue logged](https://bugzilla.mozilla.org/show_bug.cgi?id=800355) against that. In the meantime, if you want to use it on one of your projects there is [a cool polyfill](https://github.com/Polymer/observe-js) that you can use with [Polymer](http://www.polymer-project.org/).

##Why is this important?
So far, if you want to use the awesome feature of two-way data binding you have to use a framework like AngularJS, EmberJS or Backbone. All three are amazing (i prefer Angular and Ember) but AngularJS is using dirty checking, which can be very expensive especially in big complicated projects, and Ember and Backbone are using JQuery event emitter system (which i find annoying because it bloats unnecessarily your project and because it's 2014 and i can't believe we still rely on JQuery). Other options are getter/setters but that's something you need to call and it's not very neat.

With Object.observe in the game you don't need any framework for two-way data binding. You can implement the feature on your own, very easily and avoid bloating your project with a framework you don't need. For big projects, that have a lot of complicated business logic, that's invaluable because most frameworks are opinionated and that will inevitably lead you to start fighting the framework. Also not adding a big framework can leave you plenty of space to use other, smaller, better suited frameworks like Polymer or others. 

But even if you like your frameworks (and i love working with Angular so far) Object.observe will make them faster, more efficient and it will allow the developers to remove hundreds of lines of unnecessary complicated code. I can feel the joy of that developer that will delete these lines of code and commit it to the repository. That will make your framework smaller and finally allow the developing team that maintains the framework to focus to other important features. Everybody wins!

##Last thought
I am very excited about the future of Object.observe and ES7 in general. I think that features like this solve problems we've been dealing for so many years and it will help us get away from big frameworks and start finally coding full projects in vanilla JavaScript, using the right tools. We can finally stop using a hammer (JQuery) for everything and start being precise by using a scalper (Polymer). 