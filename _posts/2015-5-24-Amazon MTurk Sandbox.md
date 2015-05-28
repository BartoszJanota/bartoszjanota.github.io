---
layout: post
title: Sandbox, what is Sandbox in fact?
categories: [gsoc]
---

Have you ever heard about the *sandbox* term in a software development context? If not, this is the article exactly for you, 
nevertheless, if you know some sandboxes, this post introduces another one, maybe a new one for you.

Sandbox may refer to a box containing sand, especially one kept on a train (historically, to hold sand for sprinkling on
to slippery rails) or just to a children's sandpit. But here we will talk about sandboxing in software development. Wiki [says](http://en.wiktionary.org/wiki/sandbox):
>An isolated area where a program can be executed with a restricted portion of the resources available.

I agree with this definition of course, but in my opinion, it doesn't say the most important thing:

**Sandbox is a virtual space in which new or untested software can be run securely.**

What does it mean in fact? Sandboxes should be always introduced when one wants to expose a public API for the others. It allows
users to test their own API implementations, and it is very, very useful.

###Amazon Mechanical [Turk](http://en.wikipedia.org/wiki/The_Turk)
[MTurk](https://www.mturk.com/mturk/welcome) is a crowdsourcing platform. Main idea of this platfrom is to coordinate the 
use of human intelligence to performe simple tasks which are totally unsolvable for current computers (or very hard to solve).
The best example is a task like that:</br></br>
![Source: http://whenonearth.net/wp-content/uploads/2013/11/tree-climbing-goats-morocco-woe1.jpg]({{ site.baseurl }}/images/goats.jpg)
How many goats are there shown in the picture above?

I'm pretty sure that even the best clusters for image recognition in the world will have some problems to recognize the brown goat in the middle.
As you can see now, you can count these goats in 5 seconds and it is super easy for you.

MTurk introduces two types of users. The Requesters are able to post tasks known as HITs (Human Intelligence Tasks) and the Workers can then browse among existing HITs
and solve them (for a payment set by the Requester).

![MTurk]({{ site.baseurl }}/images/mturk.png)

One can use MTurk site to post or solve tasks, or just use an open API which is not as limited as site is. This the perfect moment when MTurk Sandbox should be introduced.

###MTurk Sandbox
OK, now we know what Mturk is, so let's try this!
But wait, probably you don't have any real tasks or you just don't want to pay cash for just an example.
Can you see the solution now? MTurk exposes sandboxes, for requesters and for workers. What is really important,
you should log in to the sanbox system with your real account. Sandbox environment is similar to the main one. Using sandbox
should be transparent for end-users. It has the same functions as the real environment or even more - because beta tests or something.

MTurk has two sandbox websites, first one is for requesters - [requestersandbox](https://requestersandbox.mturk.com/), 
and the second one - [workersandbox](https://workersandbox.mturk.com/) - for workers.

As you can see below I logged into the MTurk System as the Worker and created a post. It is well indicated that one is using the Mechanical Turk Developer Sandbox.

![Sandbox_post]({{ site.baseurl }}/images/sandbox_post.png)

I'll mention it again - you can do whatever you want with sandbox system, everything there is fictitious, so don't worry and experiment as mush as you can.

Of course now you can log in as the Worker role and take your own task. It is so simple, just try it for free!

![Sandbox_worker]({{ site.baseurl }}/images/sandbox_worker.png)

As I said before - have a look at the price, it is ridiculously high and there are no consequences!

I suppose you're getting now the idea behind sandbox systems. It is pretty useful. What you can see here is just the beginning.
You will appreciate sandboxes when you start coding your own implementation of the API. While creating software, developers must call API thousands of times.
Developers often make bugs during the development process, or just have implemented only few functions of the system. In such situations it is impossible to use
the main system, isn't it? It is nothing worst than interrupting other people work. Please always remember to respect other users of the main system! 
Thanks God, sandbox is the answer for dev's troubles :)!

###What next?
In the next post I'll show you how to use MTurk Sandbox in practice. I'll run some samples against this system.
I hope I introduced you to the MTurk ecosystem and its sandbox.

Stay tuned :)


