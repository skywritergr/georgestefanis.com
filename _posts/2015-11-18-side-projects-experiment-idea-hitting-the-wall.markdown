---
layout: post
title:  "Side projects: From experiment, to idea, to hitting the wall"
date:   2015-11-18
categories: blog
comments: true
---

For the past 6 months I’ve been working on a new side project. It all started when i wanted to learn a bit more about BackboneJS. Even though backbone is very mature, i didn’t have the chance in the past to work a lot with it and i wanted to see what it can do. I also started looking at offline first applications and this is how i got into PouchDB/ CouchDB ecosystem. So here I was, playing with two different technologies at the same time. And then it dawned on me, what if I combine them into something useful, but what?

##Solving your own problems

Finding the next billion dollar idea is next to impossible, simply because you don’t know what works for most people and what doesn’t. Some say that you should try to create a new market/niche, [create a monopoly](http://zerotoonebook.com/). To do so you should try and do things like solving big problems. Elon Musk is the master of doing that, but for the rest of average Joes, like me, it’s hard. Also, you don’t even have to solve a billion dollar problem. Solve any problem. So I might not know what’s the next billion dollar problem to solve is, but I know some of my own, silly, problems that I’d love to solve. One of them is a place where i can store all my project ideas.

##Storing project ideas

For the last 3 years i’ve used all sorts of software tools to store my ideas for future projects and experiments. They broadly fall within two categories: Note-taking apps and to-do lists. Note-taking apps make sense as the obvious place to store your project ideas but my problem is that they are being lost between other, random, notes that I make. Search works but the problem is that you don’t see them immediately upon opening the app.  Out of sight, out of mind as they say. As a result of that i tend to forget the ideas and also my note taking apps eventually become  a mess (tags etc don’t work for me).

To-do lists are awesome, for people that like lists. I don’t like lists, they stress me out. I don’t write my tasks in a paper, never did. Historically I’ve been working in my own chaotic manner. The only thing that has been working for me pretty well is [workflowy](https://workflowy.com/). Workflowy is an awesome bullet list/note taking app that helps you get organised. It’s an excellent hybrid that i love using and it’s the closest i’ve ever been into using a toDo list. The next best thing after workflowy is [Trello](https://trello.com/georgestefanis/recommend), but even that didn’t inspire me enough. So why don’t i use workflowy? I could, but I’m having the same problems I have with note-taking apps. My ideas are getting lost between chores, daily to-dos and random notes. Finding them takes some time and overall it ends up being even more distracting than note-taking apps.

Finally, the other big gap that I’m having is reminding me of those ideas. Even with storing the ideas in ways that could actual work I eventually forget to look at them. Ever. So I end up with a big list of ideas and experiments that eventually get outdated or I’m not interested on them  anymore. So the list keeps growing. So what i wanted was a mechanism that will remind me every now and again that I haven’t worked on project A in a while or never started experiment B. A motivational mechanism to make me move, do more stuff. So that’s the other part of the problem i’m dealing with.

##Combining the experiment with the idea

Starting a project from the technology and then moving to the actual idea is a typical recipe for disaster that many developers do. At the same time though it’s an excellent way to learn as many things as you can. It’s a great playground to combine skills you have with skills you wish you had. So in my case along with [BackboneJS](http://backbonejs.org/), [PouchDB](http://pouchdb.com/) and [CouchDB](https://couchdb.apache.org/) i also added in the mix [SASS](http://sass-lang.com/) for my styling and a new layout based on the “[Le Corbusier Modulor](https://en.wikipedia.org/wiki/Modulor)” design principle. That’s a lot of new stuff to use but why not? My existing skills in Javascript did help a lot, it was the glue.

On top of that I wanted to utilise my newly acquired skills in PhotoShop ( I did a course earlier this year), so i decided to start the project with a rich wireframe in Photoshop. That’s an excellent way to start moving the idea from pen and paper to actual form. So I did start doing that and here’s the first result of the main page (add an image). It’s not great and it changed a lot but still i felt good about it. One, I did it in Photoshop and two, it serves as a reminder of my original idea. One last thing, I did that bulb logo. All by myself!! I know there are designers out there that laugh their asses off now but for me it’s huge. Mad skills!!

![App PhotoShop Wireframe]({{ site.url }}/assets/brainip-sm.jpg)

##Technologies, Design, Lights… GO!

So after defining the things i want to experiment with and did the wireframe I was ready to go. And i did go! I did start working with BackboneJS, added [Marionette](http://marionettejs.com/) and [BackbonePouch](https://github.com/jo/backbone-pouch) in there too. At first i was slow, had all sorts of issues but following the advice from [The Martian](http://www.andyweirauthor.com/books/the-martian-tr/the-martian-hc) I did start solving one problem at the time and after a while i had solve so many problems that my app was functional. It was storing my ideas locally, which meant that I didn’t have to be online, and when i was online again it was synchronising with the CouchDB automatically. Beauty. I also wrote unit tests! Great!

The next step was the CSS part. SASS is a great tool and after getting used to it (especially mixins and variables) I loved it. It made things a lot easier, especially responsive design things. I was on a roll. And then I stopped. I did hit the wall, almost the same way a marathoner hits the wall towards the end.

##Hitting the wall

I stopped working on my project for almost 2 months. I was doing small things here and there but nothing significant. I open my IDE, look at my code and then i go back to youtube watching videos. The main feeling that I’m getting is that it’s pointless. First of all no one will like it, let alone use it. Then, if a developer looks at my code on Github (I’ll put it there eventually) will get really judgemental about not using best practices, or how I’m not using the framework correctly, or that half of my code is pointless. The worst bit is that they probably going to be right. So all those things kinda make me feel disappointed.

Deep inside I know I’m thinking nonsense. I know that it’s the impostor syndrome that kicks in. I know that what really matters is delivering something. Completing something is all about proving to yourself that you can commit to something and do it. It’s also something to keep your skills up to date and fuel your creativity. So there I am, exposing my idea and promising to myself that I will finish it soon. It will take some months but I will finish it. And then maybe someone else, other than me, might find it useful.

So keep in touch.
