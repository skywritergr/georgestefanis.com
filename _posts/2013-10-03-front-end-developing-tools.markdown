---
layout: post
title:  "Developing front end apps. The tools i use"
date:   2013-10-03
categories: blog
---
Front End developing has changed massively the last couple of years. The introduction of amazing JavaScript frameworks, starting from jQuery to Angularjs and Emberjs, gave the developers the ability to create cool apps and rich interfaces very easily and fast. Along with the frameworks came so many tools. I won’t speak for the available tools out there, i’ll just talk about the tools I use. So here they are. 

Yeoman - [http://yeoman.io/](http://yeoman.io/)

Yeoman is a scaffolding application that helps you kick start your project. So running a simple command, from your terminal window, gives you an entire folder tree with all the necessary files you need. Also, depending on the generator you use, you get other things like unit tests and end to end tests. I use Yeoman mostly for my Angularjs developing, but there are plenty of other yeoman generators out there for other frameworks as well. Yeoman comes also with Bower and Grunt. Both are amazing tools that help you with dependency management and deploying your app. You should really check it out on their website. I have to admit at this point that i’m feeling that i’m not utilizing Bower enough, but i’ll be trying more in the future.

NPM - [https://npmjs.org/](https://npmjs.org/)

NPM is a node.js based package manager. NPM is a must have, it makes life so much easier, downloading and updating all the tools i’m mentioning here is as easy as it can get. You will need node.js installed on your system to work, but it works equally well on a mac, windows or linux system. Nuff said, download it now!

Karma - [http://karma-runner.github.io/](http://karma-runner.github.io/)

Karma is a test runner created by Google, used mostly for Angularjs but also works with other frameworks as well. I’m using Karma in order to run my unit tests every time i do any change on my project. So like that i’m doing Continuous Integration and makes my projects more robust. I really like it, even though i have to admit it’s a bit annoying when you are trying to use it for other frameworks. I was trying to use it for an ExtJs project we are doing at work, and i still haven’t managed to make it work. I need to look more at RequireJS, but i haven’t done that yet. Also Karma plays very well with Yeoman, and the Angularjs generator automatically generates the necessary files for karma to works out of the box. Amazing!

Sublime Text 3 - [http://www.sublimetext.com/3](http://www.sublimetext.com/3)

I can’t say enough good words for Sublime. Initially i was using Eclipse, which is very bad for front end developing, and i realize i’m missing a lot. Then i moved to WebStorm but i found it unnecessarily heavy and i start looking at simple editors like sublime and textmate (I use a mac to do my developing). Even though both editors are amazingly good, i really love the color scheme sublime has, the fact that sublime can be used on my work windows machine and my backup linux developing box. Finally batch operations like refactoring code etc are amazingly easy to happen and i love it. Overall i feel at home with Sublime, i like the simplicity and freedom it gives me but it’s all matter of preference in the end of the day.

Git - [http://git-scm.com/](http://git-scm.com/)

Git is my source control of choice. I use it daily to commit code, track changes and collaborate with my friend in the US when we’re working on the same project. It’s amazing how easy it is to work with your code using correctly a source control system. I have to admit that i haven’t found a GUI tool for Git that i like so far so i’m using my terminal to do all the things i need.