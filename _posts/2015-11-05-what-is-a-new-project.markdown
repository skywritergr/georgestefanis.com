---
layout: post
title:  "What is a new project?"
date:   2015-11-05
categories: blog
---

Recently I had a conversation regarding a project I'm working on and the potential of adding more members to the (one man) team in order to [complete it faster](https://en.wikipedia.org/wiki/The_Mythical_Man-Month). The project is on top of an existing code base and the point of it is enhancing the existing functionality. The conversation started with estimating the work that needs to be done (Epics in the Agile lingo) in man-hours. After everything was estimated I mentioned that the estimated time should be multiplied by 2 because the new members will have no knowledge of the code base and they will need time to catch-up. I also mentioned that they won't be working on a new project. 

Suddenly there was tension!

## The Developer perspective of a new project

For me, a developer, a new project is a blank canvas. It's that beautiful empty folder that waits all your amazing code to be written. Your lean back-end service, that communicates with its own resource and exposes a beautiful RESTful API. No previous dependencies, not legacy code tightly coupled. A new project is a beautiful component on your Front-End that uses the new service and provides value to the user. It's robust, tested and overall a joy for everyone. In this ideal world the developers are proud for their work, the users are happy because the new feature is working great and the QA is happy because everything is tested and it's working great. All happy! That's my view anyway.

## The managers/business perspective of a new project

For the management what I described above is not a new project. A new project is something that doesn't exist currently. And technically that's right. If it doesn't exist, and you are developing it right now then it's new (even if you are enhancing an existing platform). I can't really argue with that, pure logic. The problem here is though that in developing terms this isn't new. This is building on an existing platform that has big dependencies, it's tightly coupled and requires from new team members to really learn the quirks of the new code base they are working on.

## The user

The important part here is the user. If you are lucky enough, the user won't ever know whether what they use is a micro-service, or a REST API or a monolith or has the latest shiny framework. They won't know, and won't care, whether your code is tested or not. They are here to press that button and get the expected result back. In a timely fashion. So we need to get there but while we get there we should try a few of things:

* Have fun while we do it.
* Do it in a way that ensures the maintainability of that piece of software for a long time.
* Educate and improve ourselves.
* Deliver more to the user that they expected.
* Ensure that future deliveries are going to be faster and more efficient.


## The middle ground

There is always a way to bridge the gap between developers and business people. Instead of developing on top of your huge code base spice things up. Take a small risk, trust your team, and create a new smaller service/project. Work on it and deploy it along with your big project. Even if you are sharing some resources (the database for example) and even if you don't do any TDD (because ain't no time for this!) you still did something new that checks most of the boxes in my above list, while being time conscious. Worst case scenario you'll be slightly late but it's really unlikely because your team will be empowered and motivated. Congrats! You just planted a seed. Now take care of it and watch it grow to something big.

That been said, I might be wrong and overoptimistic (typical developer treats). I'd love to hear your views.