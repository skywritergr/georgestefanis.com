---
layout: post
title:  "Getting Started with React: The very basics"
date:   2016-01-10
categories: blog
---
React is a, fairly, new Library created by the awesome people at Facebook. React is an excellent library for creating components and use it as the V in the MVC. React is easy to use all by itself or use it as part of the BackboneJS application, or any other way you fancy. That versatility is what makes React awesome. Also you can create mobile applications using React native, which is really great. 

So how do you get started? I’m assuming here that you already know some javascript. If you don’t you’re better of with another tutorial, [learning Javascript](https://www.codecademy.com/learn/javascript). It’s great if you have some experience with other frameworks, like underscore, JQuery or Angular, but it’s not mandatory. Also I’m assuming you have node and npm installed on your machine. If not you can find some help [here](https://docs.npmjs.com/getting-started/installing-node). 

## Learn the basics
If you search google for React tutorials you’ll get all sorts of results but none of them is really simple and descriptive for beginners. I found out that the best place to start is the [Facebook React Tutorial](https://facebook.github.io/react/docs/tutorial.html). This is really simple to start with and you’ll end up with a boilerplate of sorts that you can start expanding on. [Here](https://github.com/reactjs/react-tutorial) is the code that you’ll produce after completing the React tutorial. 

## Expand on the tutorial: Separating the code in an external file
This might sound trivial but it’s the very first thing i wanted to do, but strangely I didn’t get it at first. My main confusion was the type of the script. For react the type is text/babel instead of text/script that you usually would see. This isn’t just a technicality, it’s actually very important because we need to compile the JSX code to Javascript. In my case i chose Browserify and gulp to succeed that. You can also choose [webpack](https://webpack.github.io/) . I’ll show you how to do it with browserify. 

In your public folder create a build directory. That’s where we’re going to build our JSX to Javascript. We’ll be exporting a file named bundle.js
Change your index.html file to point to the above file. Your final index.html should look like so:

{% gist 269e3dee7492a5951fc3 %}

Next is creating our gulp file. In the root folder create a **gulp,js** file that contains the following 

{% gist e3ba335b580990a3ea82 %}

Then create a gulp folder and inside that folder create a new file named **browserify.js**. In the file copy the following

{% gist e802ba49ab5799b058a2 %}

Now, if you’ve used gulp before you can go into the command line, navigate to your project folder and type **gulp** and the gulpfile will run. You’ll probably going to get some errors because you’re missing things like watchify, reactify etc. So we need to to install those.
Type the following to your command line:

* npm install -g gulp (*if you’ve never used gulp before*)
* npm install browserify
* npm install gulp-concat
* npm install reactify
* npm install watchify
* npm install vinyl-source-stream
That should do the trick. If you run gulp a new file named bundle.js should be created.

If you open your file at this point in the browser your should be getting the same results as before. Good!

*Note: The way your gulpfile is right now has a minor issue. If something goes wrong with your file, or your code or anything around that area the bundle.js won’t be generated and gulp will not throw any error whatsoever. It can be frustrating at times. So if your bundle.js isn’t generating you’ll need to debug it.*ß

## Expand on the tutorial: Separating the code into multiple external files
The next logic step, that you might be thinking, is separating the classes into different files. In a big project that would make a lot of sense, and also it could help reusing code. My first thought was to just cut/paste the class in a new .jsx file and then require it from my main file. Run browserify and watch it fail.

Not to worry though, because [webpack](https://webpack.github.io/)  is here to save us. Webpack is similar to browserify but it has the added benefit that you can separate your different modules and use them wherever you can either with [CommonJS](http://requirejs.org/docs/commonjs.html) or in [AMD](http://requirejs.org/docs/whyamd.html). This is exactly what we want and it’s not that hard either.

On your root project folder create a new file called **webpack.config.js**. It should contain the following:

{% gist fb09073e6606b4c51f19 %}

_Note: if you run webpack for the first time you'll need to run **npm install -g webpack**_

Next separate the classes into different files. Leave the main.jsx just for React.render function. [This is](https://github.com/dreyescat/react-tutorial-webpack/tree/master/src) how your files should look after you’re done. If you open each individual file in this repository you’ll see that we’re requiring all our different dependencies. 

The final step is running the command **webpack --progress**. That should create a bundle.js file into your /public/build/ folder.

And that's it! There you have it. You did the basic tutorial, you then seperated the code in a different file and then splitted it into more files. You should now have an idea about react, Browserify and Webpack. In a next tutorial we'll make a new component, based on the Facebook tutorial, and next we'll see how to use it in different frameworks to enhance your existing projects.

## More reading
Want to read more? Here are some nice resources I've found. Leave more in the comments down below and I'll add them.

* [ToDo MVC](https://github.com/tastejs/todomvc/tree/gh-pages/examples/react) is always an excellent, and familiar, example to begin from
* [scotch.io](https://scotch.io/tutorials/learning-react-getting-started-and-concepts) tutorial series on react. Really nice resource.
* [egghead.io](https://egghead.io/series/getting-started-with-redux) has some very nice video tutorials on redux that are really helpful learning more both about Redux and React.