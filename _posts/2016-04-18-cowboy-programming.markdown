---
layout: post
title:  "Cowboy Programming"
date:   2016-04-18
categories: blog
comments: true
---
Recently i stumbled on [this](http://www.evanmiller.org/why-im-betting-on-julia.html), fairly, old article from [Evan Miller](http://www.evanmiller.org/) talking about [Julia](http://julialang.org/) programming language. It’s a nicely written article about the strong parts of Julia and it’s worth your time. Early in his article, Evan, mentions cowboy programming as a method that most developers are using to quickly create something that works. I am doing the same and i bet you do too.

According to Evan this progress has three main stages. The first stage is making something work. The second stage is making it fast and the third making it scream. Here’s my interpretation about these three stages and what I use for each one of them.

## Making it work

This is the first stage. You have an idea of a neat project, something that will improve your life or whatever. You need to put it in front of some people and explain to them your vision. These people can be your friends, potential clients, investors or anything in between. To do so you need something rough that just works and you need it fast!

For situations like that, as Evan says, people tend to use Python, Ruby, R or NodeJS (which is my personal favourite). These languages are all excellent candidates to help you do something really fast. For most of my projects i write a simple backend API in Python (using flask) or NodeJS (using ExpressJS) to help me iterate fast. To be even faster I have a couple of boilerplates on my Github account that I use as starting points.

##Making it fast

Making it fast is one of the first problems you need to solve when your idea is out there. What happens, usually, is that there are certain bits in your code that behave like bottlenecks. There parts need to be rewritten using a programming language that’s good in solving your specific problem. The go-to choice for many people around that is rewriting bits and pieces in C or some functional programming language (Clojure, Erlang, Scala etc).

A recent example is a piece of code, in a Java codebase, that wasn’t written with concurrency in mind. Unfortunately the time has come that this piece of code is a huge bottleneck and needs to be rewritten with concurrency in mind. Taking into account the fact that project is based on the JVM Clojure and Scala were obvious candidates. Also both of those languages are made with concurrency in mind, and they make solving these problems way easier that Java threads. We’re probably going to use Scala for various more reasons but I hope you get the point.

The thing to point here is that this is natural. Every piece of software is written with big unknowns in the picture. You don’t know many things, you don’t know how the product will change. In a sense, software is like a living organism and the environment around it affects it so much that change is inevitable. It will either mutate towards the right direction or it will die.

##Make it scream

This is the part where the interpretation of Evan’s initial post isn’t clear to me. I suspect that Evan talks about performance. In this case things like optimizing things like the JVM or writing really low level code (assembly ) makes a ton of sense. These are hard problems and also, in my opinion, edge cases. I’ve seen banks doing it a lot, in areas around micro-trading etc. I’m also aware for big companies doing it for some super critical systems but overall I think that it's still an edge case and most companies won’t need to write assembly.

I will hijack the term though because I like it. In my opinion to make something scream is to make it so beautiful, so compelling that people will want to use it just to interact with it. Then comes the hard bit of keeping them around, but that’s another story.  So, to make something scream the obvious (only?) choice is Javascript and CSS. The problem with that monopoly though is that developers abuse it. We end up creating bloated and slow interfaces that focus too much on the aesthetics or the speed of delivery. In the process we use an absurd amount of frameworks that overcomplicate things.

My go to solution these days is using ES2015 Javascript as much as I can and for the rest smaller libraries like ReactJS etc. I try to avoid big opinionated frameworks and advice against using them blindly. Also I like using SASS for big projects but for smaller projects a [well structured](https://smacss.com/) stylesheet is more than enough.

_P.S I don't like the term cowboy. It underestimates the work at hand and the craftsmanship behind it but it's a catchy title. :)_
