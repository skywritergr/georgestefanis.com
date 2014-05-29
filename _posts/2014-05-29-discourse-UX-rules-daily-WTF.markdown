---
layout: post
title:  "Discourse, breaking UX rules and making me think"
date:   2014-05-29
categories: blog
---
About a week ago i had a small exchange of messages with [Jeff Atwood](http://blog.codinghorror.com/) regarding his new start-up [Discourse](http://www.discourse.org/) and the forum of my favourite website [The Daily WTF](http://what.thedailywtf.com/). But let me start the story from the beginning. 

The daily WTF is a very popular site that posts crazy stories from the corporate life of different people, mostly in technology. Many of us relate with them, and as a natural consequence it has thousands of readers. The nature of the site is such that the community needs to share similar experiences and somehow do a group therapy for them; that's why having a forum is a good idea. So far that forum was hosted using PHPBB but it was getting old and the owners decide to move on. And they did, the decide to go with discourse. 

Discourse is the new start-up of Jeff Atwood and their main focus is to take the concept of a forum and modernise it by removing deprecated, in their opinion, conventions. The main convention looking to remove and revolutionise is the pagination. Generally speaking Discourse looks like a hybrid between a forum and a site messaging section. The users can vote for comments, reply and eventually what you get under a post is the top replies. This way you avoid all the spam, troll, hate messages and instead you get quality content. Or at least that's the idea.

To be honest curating a forum community is hard and in many cases a full time job for more than one people. Discourse is a self organised tool/forum, kinda like [StackOverflow](http://stackoverflow.com/), and that decision makes sense. In the forum days it wasn't uncommon moderators with low post count and low credibility to shut down very active, and respected, users just because they could. Entire communities were alienated and eventually lost some of their glam. It won't change the fact that some people have an authority problem, but it promises to mend it.

Having all that in mind, The Daily WTF decided that discourse was the best option. As it happens though, whenever you introduce something new to the users, the users object. And that is called [resistance to change](http://hbr.org/1969/01/how-to-deal-with-resistance-to-change/ar/1). But the users are not always wrong, there is a lot of truth in their objections. The problem is though that one of the main objections is the foundation of Discourse, getting rid of the pagination. 

Pagination has been with us since the very early days of the web and it's so natural to the users that they don't need to ask themselves how to use this. This is obeying one of the basic principles of User Experience that says ["Don't make me think"](http://en.wikipedia.org/wiki/Don't_Make_Me_Think) (Steven Krug is responsible of that simple, yet amazing, principle). Trying to get rid of pagination, the guys in discourse, broke that rule and went a different way. Instead of pagination you have a message progress bar and a summarise button that are taking the place of the pagination. 

The problem with that though, in my opinion, is that you are not able anymore to quickly jump somewhere in the middle of the conversation. I found my self plenty of times going back 2 pages in forum to see where the argument started (it's the internet, remember?), but according to Jeff Atwood arbitrary pagination is irrational.

I couldn't disagree more though because human searching tends to follow the [divide and conquer](http://en.wikipedia.org/wiki/Divide_and_conquer_algorithms) technique, where you randomly jump in a page and if the thing you are looking is not there you either go back of forth. That's mainly true when searching catalogues, but it's also true if you've been following a conversation up until last night, and you want to continue following it today.

The true essence of the matter though is in the following [article](http://www.nngroup.com/articles/satisficing/?utm_source=Alertbox&utm_campaign=558165eec8-Alertbox_email_03_31_2014&utm_medium=email&utm_term=0_7f29a2b335-558165eec8-40103213) that captures what is really all about, the users. "Most site visitors won't read all of the content provided but settle for a “good-enough” answer." and that is why it's entirely possible for users to navigate in the middle of a huge thread, to find a good-enough answer.

Finally Jeff Atwood asked a valid question. Who reads the content? And i also ask, when is the content read? Because depending of the user group that reads the content in the present time there might be no need to arbitrary pagination. But what if we're talking about a technical conversation to solve a problem, and a user is going through that 2 years later? Then arbitrary pagination is your best bet (search will get you to the conversation, eventually you'll need to guide yourself around manually).

The twitter conversation can be found [here](https://twitter.com/stefanisg/status/469608962946785281).






