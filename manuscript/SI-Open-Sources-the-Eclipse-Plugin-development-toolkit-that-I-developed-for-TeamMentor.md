## SI Open Sources the Eclipse Plugin-development toolkit that I developed for TeamMentor

For the past couple months I have been working on a Eclipse plug-in for TeamMentor (see [Programming Eclipse in Real-Time (using an 'Groovy based' Eclipse Plug-in)](http://blog.diniscruz.com/2013/08/programming-eclipse-in-real-time-using.html) , [Opening up a native Chrome Browser window inside Eclipse (raw version)](http://blog.diniscruz.com/2013/09/opening-up-native-chrome-browser-window.html) , [Injecting HP Fortify Eclipse Plug-in Views into HP's WebInspect UI](http://blog.diniscruz.com/2013/09/injecting-hp-fortify-eclipse-plug-in.html)  and [Two Videos showing TeamMentor Eclipse Plugin integration with Fortify Eclipse Plugin (as shown in HP Protect 2013 conference)](http://blog.diniscruz.com/2013/09/two-videos-showing-teammentor-eclipse.html) ).

I had a number of culture chocks coming from a C#/VisualStudio/O2Platform/REPL world into a Java/Eclipse one. The biggest one by far was the loss of 'semi-real-time' code execution that I have in Windows/C#. I used the O2 Platform REPL (and Resharper+Ncrunch VS plugins) to have a proper TDD development mode (i.e. high effectiveness and productivity), and in the Eclipse world (specially in plugin development) I had a 10 to 30 sec delay before seeing the result of any code or UnitTests execution! (which is 95% slower than what I was used to)

So, as I guess it is typical of me, I didn't just create an Eclipse Plugin. I created an _'Eclipse Plugin to create/develop Eclipse Plugins'_** (think of it as a _'Groovy based Eclipse Plugin where the Groovy scripts have access to the Eclipse Objects of the Eclipse instance running those Groovy scripts'_ :)  )

Which is basically an evolution of what you see at: [Programming Eclipse in Real-Time (using an 'Groovy based' Eclipse Plug-in)](http://blog.diniscruz.com/2013/08/programming-eclipse-in-real-time-using.html)

Now the great news is that SI ([Security Innovation](https://www.securityinnovation.com/)) as agreed last week (during AppSec USA) to open source the 'Eclipse Plugin Builder kit' part of the 'TeamMentor Eclipse Fortify Plugin'. Which is great news since it will allow for this technology and technique to be used for a much wider audience, and maybe even to be part of the Eclipse/Groovy codebase one day.

It also has lots of good benefits for SI, which is of course a for-profit company and needs to base its decisions on solid commercial decisions. As you can see below (in the email I wrote to SI) there are lots of synergetic benefits for SI to open source the 'Eclipse Plugin Builder kit' (i.e. this is a good example of when the community needs and business needs are aligned, and we have a win-win scenario).

There will be an official announcement over the next couple weeks, the code will be more cleaned up, and documentation will be written.

Meanwhile, and just for record, here is how it happen (so that others can see how 'easy' it is to open source apps developed internally)

**Step 1) have the code already in GitHub**

See [https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin)

**Step 2) make the business case internally and get a YES**  

Here is the email I sent internally which lead to the _'ok do it'_ answer

> Greetings from AppSec USA

> I know there has been a number of threads on this, and I think the time is right to wrap this up.

> In a nutshell the current TeamMentor Plug architecture is one where:

> - 95% of the code is on a 'Eclipse Plugin Build Kit'  
> - 5% of the code is on the 'Fortify specific integration'

> I.e. when the plugin starts there is nothing 'Fortify specific to it' . It is only after Eclipse loads up that the 'Fortify specific bits' occur

> So what I'm talking here is to Open Source ONLY that 'Build Kit' and keep the Fortify bit private, and actually SELL and Distribute the 'specific TM integration with products like Fortify'.

> I think this is the best of both words specially since it would still allows us to:

> - be able to charge for any plugin we develop, e.g., Fortify, Checkmarx  
- do not give away TM content for free   
- enable 3rd-parties to develop a TM plugin w/o our engineering resources, e.g., Parasoft, Coverity, Klocwork

> I can argue that the benefits are even greater (think about developers having an 'TeamMentor' tab on their Eclipse dev environment), but I wanted to cover the areas of concern.

> Now the only caveat is that we have an opportunity today to launch this at AppSecUSA to a really great audience.

> Today I'm doing an O2 Platform presentation from 10am to 11:45am and that would be the perfect place to 'announce this'

> So if we can reach the agreement to open source the 'Eclipse Plugin Build Kit' today, I can already announce it and talk about it with a number of target companies that would want to use it: e.g., Parasoft, Coverity, Klocwork, WhiteHat , etc..

> I'm around to talk if you want :)

> Dinis

To put this into context are a couple important points:  


* Although there had been multiple talks internally before on the 'business model of the plugin' there was no firm decision about it
* There were already a number of key SI player on both camps (the 'lets open source it' and 'lets sell it')
* Key in making this happening was to make sure that the concerts of the 'lets sell it' where addressed directly

  * Basically it is critical that such decision is based on solid business decisions and what is good for SI
  * Remember that SI has been paying me to write the code that has now been open sourced, which in effect means that SI has been paying for the development of Open Source software

* I didn't plan to 'push' such decision at AppSec, it just happened and  I just had a felling/instinct that that was the right moment to do it
* SI is a very unique company where ideas are given a fair chance of success, and this is another good example of it

**Step 3) Once the YES is obtained, make it public as soon as possible**  

In my case I was able to talk about it at the O2 Platform presentation I was giving (with already a number of attendees interested in helping) and start informal conversions with 3rd party companies that were at AppSec about their use of the 'Plugin Development kit' to create/extend Eclipse Plugins for their products.

Note that at this time I hadn't actually changed the license (which I have now done), but I believe that in this industry trust is an asset, and that reverting such decision would be a lose-lose situation for everybody involved.

**Step 4) Changing the license and Opening up the code (make the repo public)**  

To make it 'official' all I did was to add the [license.md](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/blob/master/license.md) file (screenshot below) to the  [https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin) and [https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin_Build](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin_Build) repositories:

![](images/Screen_Shot_2013-11-24_at_15_23_17.png)

Note that although this will be cleaned up in the coming weeks/months, this file (on an open repo) makes it official and pass the 'point of no return'.

This is what I mean to individuals/companies when I say that they should_ 'Open source sooner rather than later, and just do it!'. Since all it takes (to kickstart it) is to add a license file and open up the repo (in this case the repo was already open).

And guess what happens after such move, NOT MUCH, so if you are in a similar situation (you know who  you are), JUST DO IT!

Note this is one of those moves that has to happen, since what the process of making it open really does, is that allows for people/companies that would like the be involved, to finally start thinking about how/where/where they should do it (i.e. the sooner this process starts the sooner something real can actually happen).


**Step 5) Build community, document and officially release it**  

Which is what is coming next, so if you want to help, please join the party and lets dramatically simplify the process/effort of creating Eclipse plugins :)

I would love to see tons of forks and usage of this Eclipse Builder Kit, specially since this now brings the O2 Platform REPL environment to Eclipse, which means Java, which means OSX and Linux :)
