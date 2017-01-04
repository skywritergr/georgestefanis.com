---
layout: post
title:  "Why frameworks like ReactJS have the HTML in the JavaScript?"
date:   2016-10-06
comments: true
categories: blog
---

**TL;DR** We keep the html in the javascript prerendered in order to achieve server side rendering and not track change. Makes our lives easier and our software less error prone.

A friend of mine recently start looking at modern JavaScript frameworks for a new project that he’s starting. I told him to look towards ReactJS and Angular 2. He also has a long love towards EmberJS so that was in the options too. After looking at it for a bit he came and asked a question that I haven’t thought of. Why do frameworks like React put the HTML in the JavaScript code? I really didn’t have a good, compelling answer, other than server-rendering is all the rage lately (and I hate it when that happens). So I looked at it.

One of the main problems frameworks are trying to solve is change detection. So when the classes of an element are changing, or when a bound variable changes the framework needs to know in order to then render that new change to your browser. Angular detects changes after the fact, Ember detects changes by controlling the data model and React by re-rendering the entire, relevant, component. As a little extra, React with Immutable data is a bit smarter and it has the ability to skip components that haven’t changed all together. But I’ll focus on React since this was the firestarter in my friends question. Why put the HTML in the JavaScript?

## First, the virtual DOM

So we have the DOM, we have the shadow DOM and now the virtual DOM. The virtual DOM is essentially a JavaScript data structure that represents the real DOM by creating custom objects and then pushing them in the data structure. This way we have the entire DOM in a structure that we can easily manipulate (push, pop etc) and more importantly compare. You can read more about the [React (virtual) DOM](https://facebook.github.io/react/docs/glossary.html)

## The React way

So React, using the virtual DOM and by having the entire component HTML in the JavaScript, does re-render the entire component every time there is a change. Having the entire markup pre-rendered and ready to be returned at any point is an old practise called server-rendering. The first time i heard of server-rendering was in Python and more specifically in frameworks like Django. So hearing it again, in 2016, for a JavaScript framework really confused me. I thought that this is happening, somehow, to the backend, but here’s something you need to remember, server !== backend in this context. What we actually mean is that we have the entire DOM, prepared with all the variables in there ready to be rendered in the browser at any point.

In order for React to know though when to re-render and when not it uses a diff technique where it compares the old version of the DOM (before the change) with the new version of the DOM (after the change) and if a change is detected then it calls for a re-render. This process is called [reconciliation.](https://facebook.github.io/react/docs/reconciliation.html)

The above sounds like a very suboptimal solution. Re-rendering everything on a simple change would normally be a O(n^3) problem, where n is the number of nodes. So for a page with 1000 nodes we would have to do 1 BILLION comparisons, which would have taken us 1 second with modern CPUs but it’s still unacceptably slow. React engineers managed to make this problem an O(n) complexity problem by accepting 2 simple heuristics:
Two components of the same class will generate similar trees and two components of different classes will generate different trees.

It is possible to provide a unique key for elements that is stable across different renders.
So if you use the virtual DOM and the above heuristics you end up with an algorithm in which you are comparing 2 arrays (the old Virtual DOM vs the new Virtual DOM). If the new DOM is from a different class React will render it, no questions asked, if it’s from the same class react will compare the individual attributes between the old and the new version. The result is that only changed components are being rendered and the entire operation is cheaper and faster. There are some more side benefits too.

## Keeping a state (or not)

Another big problem with frameworks, and programming in general, is maintaining the state of a program. This is hard thing to do and more often than not it’s the source of many bugs and an assortment of other issues. In Angular and Ember you are maintaining a state in your JavaScript and then you mix it/bind it with your templates. In React you don’t have to do that since every time a change is detected in the component, the entire component is being re-rendered. So this way your UI logic is a lot more simple since you don’t care about maintaining a state and therefore you don’t track change anymore.

## Bonus, adding a dash of Clojure in our JS. Immutable data.

Clever as it sounds, using fancy heuristics and tree traversal and all that, we can further improve the performance of React by adding Immutable data in our lives. With Immutable data, every time we change something in a data structure a new version of it is being created.  What this means is, that if the virtual DOM is in a structure that can’t be mutated, every time a change is happening we’ll have a new state in which the component will be pointing at. This enables us to skip checking the component attributes all together and move on to the next. This is happening because we know that since our data is Immutable we can’t possibly have a change in the component if we’re still using the same virtual DOM. This little functional programming paradigm helps making the reconciliation process from an O(n) problem to a O(log(n)) problem, and this is a massive improvement.

On the negative side of things, using immutable data makes pushing in the virtual DOM array slower by 3 to 5 times, but this is a constant number and the benefits from getting from an O(n) to a O(log(n)) outweigh that constant penalty in push. If you want to learn more about React and immutable data I highly recommend watching this video from ReactConf 2015.

<iframe width="560" height="315" src="https://www.youtube.com/embed/I7IdS-PbEgI" frameborder="0" allowfullscreen></iframe>

There are a few frameworks that plug on top of React to give you the power of immutable data, one is [OM](https://github.com/omcljs/om) and the other [Immutable-JS](https://facebook.github.io/immutable-js/). It’s really worth checking them out.

### More reading:

* [https://teropa.info/blog/2015/03/02/change-and-its-detection-in-javascript-frameworks.html]()
* [https://github.com/omcljs/om]()
* [https://facebook.github.io/immutable-js/]()
* [https://www.youtube.com/watch?v=I7IdS-PbEgI]()
* [https://facebook.github.io/react/docs/reconciliation.html]()
