---
layout: post
title:  "Chrome tools 101: The Timeline tab"
date:   2015-05-06
categories: blog
---

Most of the web developers I know choose Chrome as the browser of their choice to test their apps, debug and ultimately browse the web. There is a very good reason for that, and the reason is called Dev tools. The dev tools in chrome, along with the many addons, provide the developer with a platform ready to develop, debug and experiment at any time. If you haven't checked the dev tools yet, open your browser and press Alt+Cmd+i on Mac OS (or ctrl+shift+i if you are on windows or linux). You should be able to see something like this:

<img src="{{site.url}}/assets/dev-tools.jpg">

There are many tabs, you are probably already familiar with the console tab and the elements tab, but in this post i want to talk about the timeline tab. The timeline tab is an indisposable tool for identifying and ultimately fixing performance issues that you might be dealing in your application. How you use the timeline is simple, you open it and you click the button that i have highlighted above (the one that looks like a record button). After doing so you just perform some action in your app (preferably something that you know it's performing bad) and after a while you press the same button again. What you end up with is something like the below:

<img src="{{site.url}}/assets/dev-tools-result.jpg">

What you see here is the timeline from [performance.fail](http://performance.fail/) a website that i created to be intentionally slow. In the above image we see some very interesting things. Let's take it one by one.

## The Frames View

The frames view is the top bar chart that you see on the above image. The frames view is an indication on how fast or slow each frame of our app/website is behaving. For a modern, fast, performant website every developer should strive to achive a 60fps (frames per second) frame rate. You can see the frame rate highlighted above.

In our example you can see most of the bars being below the 60fps but you can also see that there are several bars that are way above the 60fps mark. In fact if you go to [http://performance.fail/](http://performance.fail/) now you'll witness yourself the site being slow and choppy. The bars above are the clear indicators on where we are having a problem. So if we want to improve the performance we know where to look.

Feel free to open the website, open the dev tools in the timeline tab, press the record button and just scroll up and down on the website. Then press the button again to stop recording. You should now have a chart similar like mine.

## The flame chart

Below the Frames view you can see some horizontal, coloured, funky bars. That part of the timeline is tha flame chart. The flame chart is by far my favourite view and i'll explain you why right away. In the frames view, if we click any bar (frame), the flame chart below will focus into that frame. What you will then see is the coloured bars getting a bit bigger and also you'll notice that there is an indication of how long it took for that frame to render and do its thing. If you go to your browser and click on any bar (pick a tall one) you should see that particular frame taking more space. Now we need to focus further.

In order to further focus in a bar you have 2 choices. The first one is to point your mouse cursor to a bar and then scroll in. If you do that too fast you might end focusing on the whitespace, but that OK. You can drag the timeline left or right by drag & drop or you can zoom out. Your other option is clicking on the bar you want to zoom in (pick a yellow one) and then press the WASD buttons. W zooms in and S zooms out. That's probably the easiest way to do it as you get more accurate.

If you focused in a yellow bar you should then see something similar like the image below. Let's explain what we see here.

<img src="{{site.url}}/assets/dev-tools-result.jpg">

The yellow bars in the timeline indicate JavaScript scripts that are running. Purple bars are style recalculation (your CSS being recalculated because of some reason). Green bars is the browser [rasterizing](https://en.wikipedia.org/wiki/Rasterisation) or painting the frame. You should have also noticed by now that the bars are stacked. This is my favourite part! The stacked bars indicate what part is cause what. So in our example you can see three stacked bars, 2 yellow ones and a purple one. What the browser is telling us is that the first script called a second script and that caused the browser to recalculate the style. Recalculating the style and forcing the browser to repaint can be a very expensive procedure and eventually hinder performance.

The final thing that makes the flame chart so amazing is that if you click on that purple bar you'll then see what part of the script caused the style recalculation, and if you click on the script name the dev tools will take you to the exact script line. Awesome! So all you need to do now is fix it either by changing your strategy slightly or finding a different CSS selector that doesn't cause the browser to paint or do the layout again, or simply fix a code bug that you might have. In order to see what CSS properties are triggering the layout and the paint you can visit [csstriggers.com](http://csstriggers.com/). 

## Summary tab

The final bit in the timeline is the summary tab. The summary tab get populated once you click on one of the bars in the flame chart. The summery tab will then show you a pie chart with the different operation the browser did in the time it took for that action. In our example you can see that the pie chart is letting us know that it 1.225ms for that action to complete (depends on what bar you clicked) and is splits down the time to Scripting time, Rendering time and other. This is very useful as it gives you an insight on what takes more time. 

Last but now least the summary tab will give a stack trace of the scripts that executed in order to get to this point. So for example if you click on a purple bar you'll see what scripts caused the browser to recalculate the style. That way you can go ahead and change that if you feel it's necessary or evaluate if you really need to run this piece of code every time. Is it a feature or a bug?

## What about those select boxes on the top?

The example i saw you above is what you get if you select the causes option of the tools. Chrome comes with more though. Selecting JS profiler gives you a lot more information about your JavaScript code but it can get very expensive and you should only have it selected if you know that you have a real problem with your JavaScript code.

The memory option is a very useful feature that lets you know how much memory you are using in your app. What happens with browsers is that every so often they deploy the garbage collector and empty the memory for you from unused variables etc. Gone are the C days where you had to care about pointers, deallocation and other devilish stuff like that. Now the browser does all the complicated stuff. If you run the profiler with the memory option selected you should get something like that:

<img src="{{site.url}}/assets/dev-tools-memory.jpg">

That graph is called a sawtooth graph and what you are actually see is the browser garbage collector emptying the memory. That is the part where the graph goes down to zero. If your graph never goes down to zero it means that you have a memory leak. This is another great way to see what you are doing wrong and where.

The final option is paint where the dev tools are capturing graphic layer positions and painted pictures but that has a big performance overhead so use it wisely and only when necessary.


## Now what?

Hopefully now you know a bit more about the timeline tab and you can use it on one of your existing projects or at work and let your colleagues know about that new bug that you found. I would suggest you go ahead and play around, start clicking things and zoom in/out. It gets better once you get used to it. 

Also if you want to learn more about web performance and building 60fps apps i can't suggest enough doing the Udacity course about [Browser Rendering Optimization](https://www.udacity.com/course/browser-rendering-optimization--ud860) that's build by Google. It will really make you a better developer. 


