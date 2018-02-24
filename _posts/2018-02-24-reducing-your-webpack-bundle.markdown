---
layout: post
title: "Reducing your Webpack bundle size"
date: 2018-02-24
categories: blog
comments: true
---
The last couple of months, [my team at Transferwise](https://transferwise.com/jobs/), has been working to deliver a new feature on our product. We call this feature Money Tracker and helps TransferWise users to track their money better. I've been developing it for the web using Angular in an external component. As a general approach for our frontend all of our new features are created in their own repository, using ES2015, Webpack and Babel.

After deploying the first versions and going through bug fixing we found out that my newly created bundle from Webpack was 1mb. This is unacceptable size for an app as large as ours (or any app really). After a bit of fiddling around I managed to drop the size of it in less than 40kb. This is how I did it.

## Investigate
The first step is to find out why your bundle is that big. The hard way to do this is by searching in the bundle outcome of Webpack for know libraries. But this is tedious and you'll miss stuff for sure. The best way to do so is by using a Webpack analyser. I ended up using [Webpack Visualizer](https://github.com/chrisbateman/webpack-visualizer) by [Chris Bateman](https://twitter.com/batemanchris).

To use it just do `npm install --save-dev webpack-visualizer-plugin` and then in your `webpack.conf.js` you need to add the following things:

{% gist 4d22d0647a8a39fcf3d62d6f8104bfaa %}

Now if you run your Webpack build job locally you will get a `stats.html` file. That will look something like this:

![Webpack visualizer pie chart]({{site.url}}/assets/webpack-visualizer.jpg)

We can see a few things here. The size of my bundle (1mb 😱) and a very nice breakdown where is everything coming from. In my case I was bundling `moment.js`, `bootstrap.css`,  `bootstrap.js` and an internal TransferWise library. All of these things for me were [peer dependancies](https://stackoverflow.com/questions/18875674/whats-the-difference-between-dependencies-devdependencies-and-peerdependencies), so I shouldn't have bundled them.

## Understand
This is the point that you need to understand where this files are coming from. There are two suspects here, libraries that you haven't marked as externals in your `webpack.conf.js` or libraries you have explicitly included in one of your files, e.g `import moment from 'moment'`. Lets look at these two things.

### Webpack externals
This is a configuration in Webpack that tells the bundler that it shouldn't pack these things, because they will be already there to the application that is going to use your new module. This is excellent for these cases where you are developing a library or a component to be used by a bigger app. By using externals you greatly reduce your bundle size.

So in my moment example I should have added the following line in my `webpack.conf.js`:

{% gist 749c75a6c864b9d31e811952f2990241 %}

Now, for bootstrap and the TransferWise library I had already an entry for them in externals, so I really wondered why they were still bundled. And that's how we go to the second point.

### Explicit imports
In my package I have central `index.js` that works as the starting point of everything. Bootstraps the component, imports necessary libraries etc. In there I had these three lines:

{% gist 9b01c407791154ef7a25cc00f2f213d5 %}

These three lines were saying to Webpack that it should really bundle them as the application needs them. That wasn't necessary though. These libraries are marked and peer dependancies in my `package.json` so the app that uses my component should already have them. So I removed them, and they stopped being bundled. It was my bad for including them in the first place.

The only caveat here is that now your tests might be failing (mine did, that's one of the reasons why I put them there in the first place). To solve that just import the necessary libraries in your test configuration file.

## Summary
So here what I learn:

* Use an analyser to see what is it that you are packaging
* Avoid explicit  import of libraries that are marked as external dependancies
* Learn how to use Webpack external externals
* Don't serve massive bundles, not everyone has a speedy connection. You are making the customer experience worst.