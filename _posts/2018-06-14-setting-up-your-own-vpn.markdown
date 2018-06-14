---
layout: post
title: "Setting up your own VPN with Streisand Effect"
date: 2018-06-14
categories: blog
comments: true
---
These days having a VPN is a very smart choice you can do. Either you work on a public space, in your office or any foreign country you are travelling. You can never be sure who is listening. Also there are certain governments that are not really friendly.

So once you decided a VPN is worth it you need to understand how it really works. In very abstract terms what you are doing is setting up a connection between your device (laptop, smartphone etc) to a remote server (the VPN provider). Once you do that all your browsing data will first go to that server and then out in the internet. So if your ISP, say, was to try and look who are you talking to, all they'd see would be some encrypted messages to a random server. They can't know that you are searching on Google about flowers.

Now, that's all fine but you need to realise one thing. In an effort to be more secure you are trusting all your browsing to a 3rd party company (the VPN provider). In the past they've beer reports of VPN providers keeping logs of your browsing and sharing them with other parties. That kinda beats the purpose of security and anonymity.

## Don't trust a 3rd party company
Yeah, don't. Why ExpressVPN or PIA is more trustworthy than simply not having any VPN? Be your own VPN provider by using one of the numerous cloud providers. 

Your options are many:
	* Amazon AWS
	* Digitalocean
	* Linode
	* Azure

Etc etc just to name a few. A lot of these providers will even give you a free year of use before you start paying. Once you are past your free year you can either look around or pay as low as 5$ per month. A worthy investment to your privacy and peace of mind. 

I prefer Digitalocean, as I've been using them for years for all of my websites and dev servers. They are super cool and they have a plethora of help articles if you decide to do something else. 

## Streisand effect + Digitalocean
Setting up your own VPN is super easy
1. Go to [GitHub - StreisandEffect/streisand:](https://github.com/StreisandEffect/streisand) and make sure you have all the prerequisites. If you are on a Mac or a Linux machine chances are you have most of the things install already (Python 2.7, Git, pip etc). I only had to install Ansible via brew (`brew install sensible` did the trick).
2. Go to Digitalocean and ([create an account](https://m.do.co/c/aaeb775a89f0))if you don't have one.
3. Login and in the top right corner click `Create`. Choose droplets and there pick the basic 5$ Ubuntu droplet.
4. Click Done. 
5. In the next screen copy your VPS IP. It will come in handy.
6. Once you are done it's time to checkout the Streisand code: `git clone https://github.com/StreisandEffect/streisand.git && cd streisand`
7. All you need to do now is run `./streisand`
8. Follow the prompts and by the end of it you should have your own VPN in your new server.

After you've done the above Streisand will auto-generate an HTML file with very handy information on how to connect  to your new VPN. It has all sorts of options.

## Streisand effect + other cloud providers
The above details are suitable for my use case. I understand that a lot of people don't want to pay the 5$ per month, or work with Digitalocean, or even do all those manual steps.

If you don't want to do that the Streisand effect developers have an more automated process that automatically generates the new servers for you. I happen to find the process a bit troublesome due to the python packages that were required. That doesn't mean that you will stumble on the same problems.

In that case all you have to do is checkout  is:
1.  Checkout the Streisand code: `git clone https://github.com/StreisandEffect/streisand.git && cd streisand`
2. Run `./streisand` and follow the on screen commands. 

Note that you still need to fulfil the prerequisites.

## Final words
Looking back to what's required I understand that this isn't a process your average user will do. This requires familiarity with the command line, cloud providers and how to troubleshoot technical problems via searching the web. Don't let that dishearten you though. If you are looking for a challenge go for it.

If all you want is a VPN then at the very least start with a reputable VPN provider. [Reddit](https://www.reddit.com/r/VPN/) is a good place to do some research in regards to what's good these days.

P.S The Streisand developers have in their list of upcoming features to simplify the process. Maybe in the near future setting up your own VPN won't be such an involved process.
