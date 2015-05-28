---
layout: post
title: Getting into AutoMan
categories: [gsoc]
---

Earlier this week I showed you how to use MTurk Sandbox, I did it via their web site. But it's not the point of the sandbox idea. 
I promised you to show how to take more advantage of this sandbox system. Today I'm gonna call MTurk Sandbox API exactly from
AutoMan code.

###Let's run the AutoMan
You could read some info about MTurk in my very recent [post](http://www.bartoszjanota.com/Amazon%20MTurk%20Sandbox/). 
Now I would like to introduce the [AutoMan](http://emeryberger.com/research/automan/) library.
This library is a smart client to MTurk, it is an easy-to-use tool written in Scala by an awesome guy [Dan Barowy](http://people.cs.umass.edu/~dbarowy/).

###Sample program
It's high time we run a sample program.     
You can read more details about using and running AutoMan library [here](https://github.com/dbarowy/AutoMan#using-automan-in-your-project), what's more, 
author of this amazing library prepared some samples for you, all you need to do is just clone the repo and have a look at [apps](https://github.com/dbarowy/AutoMan/tree/master/apps) dir.
I just created a simple app, look at the code:
{% highlight scala %}
import edu.umass.cs.automan.adapters.MTurk._

object automan_example extends App {
  val opts = Utilities.unsafe_optparse(args, "automan_example.jar")

  val a = MTurkAdapter { mt =>
    mt.access_key_id = opts('key)
    mt.secret_access_key = opts('secret)
    mt.sandbox_mode = opts('sandbox).toBoolean
  }

  automan(a) {
    def which_one() = a.RadioButtonQuestion { q =>
      q.budget = 99.00
      q.text = "Was it easy to write an example of AutoMan app and run it against MTurk Sandbox?"
      q.options = List(
        a.Option('yes, "Yes, of course :)!"),
        a.Option('no, "No :(")
      )
    }

    which_one().answer match {
      case Answer(value, _, _) =>
        println("The answer is: " + value)
      case LowConfidenceAnswer(value, cost, conf) =>
        println(
          "You ran out of money. The best answer is \"" +
          value + "\" with a confidence of " + conf
        )
    }
  }
}
{% endhighlight %}
Now we would like to run this app. Here you would appreciate [MTurk Sandbox](https://requestersandbox.mturk.com). 
You may ask why? Because there will be no bad consequences of running this program.
It is important, because now I have no idea if this program is written properly or if it finally works.
Imagine a situation when you make a mistake and post thousands of HITs to the production. And what if some real workers solve it?
What you pay for it?

###Configuration
Ok, let's go. Last time I told you that using sandbox system should be transparent for end-users. Now you can see how it exactly works.
As you probably know, to run any of the AWS services, you must provide some credentials. 
AutoMan uses [Amazon Mechanical Turk SDK](http://docs.aws.amazon.com/AWSMechTurk/latest/AWSMechanicalTurkGettingStartedGuide/Welcome.html),
so you need to provide your *Access Key ID* and *Secret Access Key* (see [more](http://aws.amazon.com/security-credentials).
The example above is adjusted to read your credentials as a program arguments. If you run program with no args, you're gonna see the error:

![automan_example_error]({{ site.baseurl }}/images/automan_example_error.png)

Meantime I got my *Access Key ID* and *Secret Access Key* connected with my account created in [requestersandbox](https://requestersandbox.mturk.com)
and prepared a proper run configuration:

![automan_example_configured]({{ site.baseurl }}/images/automan_example_configured.png)

Ok, now you may say, that this configuration is not transparent for end-users. Have a look at the code above, you must tell the program to run in *sandbox_mode*, because MTurk Sandbox URLs are different than the production ones. 
Trust me, this is an only difference:

![sandbox_mode]({{ site.baseurl }}/images/sandbox_mode.png)
![sandbox_url]({{ site.baseurl }}/images/sandbox_url.png)

Let's run this app, I hope everything is well configured, we'll see:

![automan_example_running]({{ site.baseurl }}/images/automan_example_running.png)
It seems promising, you can see your tasks defined above.
s
###Do we have a success?
Finally you can check your progress, just go to the [online HITs manager](https://requestersandbox.mturk.com/mturk/manageHITs) and look for your task,
this is what I saw:

![sandbox_HITs_manager]({{ site.baseurl }}/images/sandbox_HITs_manager.png)
And of course we have a success :)! I defined my HIT using AutoMan and MTurk Requester Sandbox. 

Let's see what happened at MTurk worker Sandbox:

![sandboxworker_HITs]({{ site.baseurl }}/images/sandboxworker_HITs.png)
Now you gusy have about 30 minutes to log in [workersandbox](https://workersandbox.mturk.com) and to answer my question:

**Was it easy to write an example of AutoMan app and run it against MTurk Sandbox?**

I hope you see the point of sandbox systems. It is pretty useful during the development process.

Thanks to that, I'm sure my development environment works fine, now I can start working on the debugger.






