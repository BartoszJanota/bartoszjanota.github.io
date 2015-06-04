---
layout: post
title: AutoMan Debugger AVD
categories: [gsoc]
---

Let's talk about the essence of my GSoC'15 participation. As you probably know guys, my main task is to
develop and deliver [AutoMan Monitoring and Debugging Plugin for IntelliJ IDEA](https://github.com/plasma-umass/GSoC/wiki/Idea-List-for-Google-Summer-of-Code-2015#automan-monitoring-and-debugging-plugin-for-intellij-idea).
The topic of my task is very descriptive, but wait, what should I actually do?

All of these things sound great, now I am familiar with AutoMan workflow and useful stuff like [MTurk Sandbox](http://www.bartoszjanota.com/Amazon%20MTurk%20Sandbox/). 
There is one thing I didn't introduce you. [Bianca Tamaskar](https://www.linkedin.com/in/biancatamaskar) developed pretty good [AutoMan Visual Debugger](https://bitbucket.org/btamaskar/automan-debugger) (AVD).
  
###AutoMan Visual Debugger
Okay, so what's that? Probably best description is an original one, so Bianca says:
> - (...) the two components of AVD: a 1) plugin implementation (an embedded web server built on [spray](http://spray.io)) and 2) a JavaScript web UI.

> - AVD is currently an alpha-quality research prototype.

So as you can see, AVD is an autonomous REST server which is simply connected with a web panel. Let's see how to use this thing and how it works in fact!

Deployment for development is easy and deeply described in [README](https://bitbucket.org/btamaskar/automan-debugger). Following README sections cover
usage and other interesting things.

###AVD in action
Creating your AutoMan MTurk program you must call `MTurkAdapter` class which is a subclass of `AutomanAdapter`. Is behaves as an interface to human-computations functions.
Basic usage of `MTurkAdapter` requires one import in your code, AVD requires another one:
{% highlight scala %}
import edu.umass.cs.automan.adapters.MTurk._
import edu.umass.cs.plasma.automandebugger.AutomanDebugger
{% endhighlight %}

Before importing anything connected with `AutomanDebugger`, remember to add a required dependency to your `build.sbt` file:

{% highlight scala %}
//assuming you have `automandebugger` package locally deployed
libraryDependencies += "edu.umass.cs.plasma"  %%  "automandebugger" % "0.1-SNAPSHOT"
{% endhighlight %}

Now you can use `AutomanDebugger`, all you need to do is to add a plugin to your adapter, all `AutomanAdapter` implementations are able to accept
a list of plugins. Look how you can do it:

{% highlight scala %}
val a = MTurkAdapter { mt =>
    mt.plugins = List(AutomanDebugger.plugin)
    mt.access_key_id = opts('key)
    mt.secret_access_key = opts('secret)
    mt.sandbox_mode = opts('sandbox).toBoolean
}
{% endhighlight %}

And that's all, it's easy, isn't it? All other things remain unchanged. Existence of AVD is totally transparent for your implementation.

In fact, AVD is a `Plugin`, this is why integration between AVD and your program is so simple.
 
###What does it look like?

Generally if you configured everything, you should now be able to check AVD in action. 
Run your program, go to your favourite browser and check [AVD web interface](http://localhost:8080) (of course if you have AVD package deoployed locally).
This is what I saw:

![AVD]({{ site.baseurl }}/images/AVD_big.png)

AVD looks like the thing people exactly need. My first impression is pretty good. Let me share my opinion?

 - On the left hand side one can see all currently running tasks - so you don't need to change context to see other tasks.
 - In the main screen all of tht data connected with a given task is displayed. It is like a current state of the task. 
   - Left column says about static and general information about the task. One the right hand side you can monitor your wallet.
   - In the middle one can see a big chart (imho the most important thing here). It says about the task completion.
   
AVD is a great starting point to plan my job. Now I can see what people need. 
You may ask: Since AVD is a good tool, so why do you exactly need to develop another one? Let me answer this question.

There are a few things me and Dan have in our minds:

 - We want to change the environment. I want to introduce a debugger as a plugin to IntelliJ IDEA (actually not only for Intellij IDEA).
 - My experience shows that it is best to present data as a set of charts, so I would like to propose the brand new layout.
 - Plugin for IDE must be very compact - it cannot interrupt the code section in IDE. We still don't know how to navigate it.
 - AVD is a one way debugger - read only some say. Our intention is to let people interact with a running ask via the plugin - in some cases of course.
 - Alarms - is it able to introduce some warnings for user and predict that something bad is happening? We will see...
 
It has been just released a stable version of AutoMan. Let me go through this and start coding things listed above :)!   
 
 





