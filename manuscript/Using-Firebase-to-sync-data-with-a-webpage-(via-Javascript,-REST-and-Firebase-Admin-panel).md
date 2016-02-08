## Using Firebase to sync data with a webpage (via Javascript, REST and Firebase Admin panel)

If you haven't seen the [Anant Narayanan](https://twitter.com/anantn) presentation on [AngularJS conference](http://ng-conf.org/) called [Building realtime apps with Firebase and AngularJS](http://www.youtube.com/watch?v=e4yUTkva_FM) you are missing something good.

[Firebase](https://www.firebase.com/) really seems to fix one of the pain points that I currently have in client-server development, which is _how to send/synchronise data across multiple clients (including the server)_.

I first heard about Firebase from the **_Wire up a Backend_** example that can be found at [http://angularjs.org](http://angularjs.org/), and today I was able to give it a test drive (since I want to use it on the AngularJS front-ends that I'm currently developing for [TeamMentor](https://teammentor.net/))

**1) Creating an Firebase account**  

Lets start with creating an account and following the [Firebase 5 minute tutorial](https://www.firebase.com/tutorial/).  

The process of creating an account is just a case of going to [https://firebase.com](https://firebase.com/)

![](images/Screen_Shot_2014-02-24_at_15_25_53.png)

... choosing a username and password (there is also the option to create an account based on an GitHub account)

![](images/Screen_Shot_2014-02-24_at_15_26_22.png)

... and that's it:

![](images/Screen_Shot_2014-02-24_at_15_27_11.png)

Firebase by default creates a test app, which can be immediately accessed by clicking on the blue _View Firebase_ button:

![](images/Screen_Shot_2014-02-24_at_15_27_40.png)

**2) Firebase tour**  

On first load of the Firebase control panel, we are presented with the offer to take a tour, which is a great way to understand the basics of how it works.

![](images/Screen_Shot_2014-02-24_at_15_27_55.png)

The first step of the tour is to add some data:

![](images/Screen_Shot_2014-02-24_at_15_28_16.png)

... directly on the current's App data viewer:

![](images/Screen_Shot_2014-02-24_at_15_28_47.png)

After we click on the **Add** button, we will see that our data is now part of this Firebase App data stream:

![](images/Screen_Shot_2014-02-24_at_15_29_05.png)

Next (after clicking on the **See it in action** link), we get this mini chat application with 3 messages:

![](images/Screen_Shot_2014-02-24_at_15_29_37.png)

If we add a new message:

![](images/Screen_Shot_2014-02-24_at_15_29_57.png)

... and look back to the Firebase admin panel, we will see the 4 messages (3 added by the **_Sample Chat Application_** and the one I added manually)

![](images/Screen_Shot_2014-02-24_at_15_30_12.png)

The final step of the tour is to make a change directly on the Firebase admin panel:

![](images/Screen_Shot_2014-02-24_at_15_30_29.png)

... and confirm that the value was _automagically_ changed in the **_Sample Chat Application_** (in real-time with no user interaction)

![](images/Screen_Shot_2014-02-24_at_15_30_48.png)

**3) Creating a simple Html/Javascript page to test it out**  

Note: The next set of example will use code snippets provided by the Firebase [Web Quickstart Guide](https://www.firebase.com/docs/web-quickstart.html)

![](images/Screen_Shot_2014-02-24_at_15_37_22.png)


Since I'm going to use Eclipse (Kepler), the first step is to create a new **_Static Web Project_**

![](images/Screen_Shot_2014-02-24_at_15_38_06.png)

... with a simple HTML inside:

![](images/Screen_Shot_2014-02-24_at_15_38_54.png)

... containing the just the **_firebase.js_** script import and a simple data setter:

![](images/Screen_Shot_2014-02-24_at_15_43_26.png)

To see this in action inside Eclipse, I opened up the admin Url in a Browser window (I wonder how long until an Eclipse Firebase plugin is created), and I logged in:

![](images/Screen_Shot_2014-02-24_at_15_43_51.png)

**4) Setting and Pushing data**  

At this stage I had the Html at the top and the Firebase admin panel at the bottom (note the required full url in the **_var myRootRefnew Firebase(...)_** Javascript code):

![](images/Screen_Shot_2014-02-24_at_15_46_22.png)

Next step was to open a Web Browser with the test page:

![](images/Screen_Shot_2014-02-24_at_15_44_23.png)

... which set the Firebase server side value to "Hello World!" (I have to say it made me a bit nervous to see how easy it was to completely remove an entire Firebase dataset (I wonder if there are backup or transaction logs for Firebase data))

![](images/Screen_Shot_2014-02-24_at_15_46_40.png)

Next step was to try setting some name-value pairs (i.e. a typical JSON string):

![](images/Screen_Shot_2014-02-24_at_15_51_46.png)

... which looked like this after execution (note that I didn't refresh the Firebase admin panel (it also uses the WebSocket technology to keep itself up-to-date))

![](images/Screen_Shot_2014-02-24_at_15_51_55.png)

Next I tried the **_push_** method (which behaves like an array and was the technique used in the chat example):

![](images/Screen_Shot_2014-02-24_at_15_54_41.png)

Here is the execution result (note how there is now an extra **_TreeNode_** with the data provided)

![](images/Screen_Shot_2014-02-24_at_15_55_01.png)

**5) receiving events**  

So far we have been setting/pushing data into Firebase, but what is also really powerful, is that we can subscribe to server-side events, and update the browser/ui when content changes.

The example below shows how to get a callback every-time a new item is added:

![](images/Screen_Shot_2014-02-24_at_16_02_46.png)

Now on refresh (screenshot below), the new children will be shown on the page:

![](images/Screen_Shot_2014-02-24_at_16_03_02.png)

One observation, when we subscribe to the _child_added_ event, any changes made directly in Firebase's admin panel:

![](images/Screen_Shot_2014-02-24_at_16_03_31.png)

... will only be seen when we refresh the page (where all items are viewed as new children)

![](images/Screen_Shot_2014-02-24_at_16_03_52.png)

To see the changes in real-time, we need to change the event to _child_changed_:

![](images/Screen_Shot_2014-02-24_at_16_11_22.png)

Now (on refresh) we get an empty list:

![](images/Screen_Shot_2014-02-24_at_16_11_31.png)

... but if the content is changed on the Firebase admin panel:

![](images/Screen_Shot_2014-02-24_at_16_11_58.png)

... the _child_changed_ event is triggered, and we will the new content changes on the browser (without page reload)

![](images/Screen_Shot_2014-02-24_at_16_12_09.png)

**5) Consuming and Sending events using REST API**  

Now that we can create and consume Firebase events using Javascript, it is time to try their REST API.

For that, I'm going to use the [Eclipse Grovy REPL Scripting Environment 1.6.0](http://marketplace.eclipse.org/content/eclipse-grovy-repl-scripting-environment) so that I can do it directly from Eclipse

Note: most scripts shown below are on [this gist](https://gist.github.com/DinisCruz-Dev/9193091)

The first test was to get the current data set, which is easily retrieved via a simple GET request to the Firebase url for the current application (with a **.json** appended to in the end of the admin url):

![](images/Screen_Shot_2014-02-24_at_16_28_28.png)


Since we are in eclipse, here is the code to open the **_JavaScript Editor_** programatically with the json data received:

![](images/Screen_Shot_2014-02-24_at_16_28_58.png)

By default the data received from the server has no formatting:  

![](images/Screen_Shot_2014-02-24_at_16_29_08.png)

But since we are inside the Eclipse  **_JavaScript Editor_**  if we assign it to a variable, we can easily format it:

![](images/Screen_Shot_2014-02-24_at_16_29_32.png)](http://4.bp.blogspot.com/-zmZwwRmTtx0/UwuKrkN2aZI/AAAAAAAAHgY/oUFf7e-ksS4/s1600/Screen+Shot+2014-02-24+at+16.29.32.png)


After doing this, I discovered that if we pass a _?print=pretty_ to the Firebase url:

![](images/Screen_Shot_2014-02-24_at_16_32_40.png)

... the received json data will already be nicely formatted:

![](images/Screen_Shot_2014-02-24_at_16_32_46.png)

In the example below I used the Groovy REPL _Execution result_ window to see the formatted json data:

![](images/Screen_Shot_2014-02-24_at_16_36_51.png)

Next thing I wanted to try was to see how a REST change would be shown in real time in the browser.

Because my next REST request will use the HTTP PUT command (which is equivalent to the Firebase **_set_** Javascript function), I changed the Html page to display and listen for Firebase _values_ (vs arrays with name-value pairs)

Note the **_snapshot.valueOf().val()_** command below:

![](images/Screen_Shot_2014-02-24_at_17_44_32.png)

After browser refresh, this is what the test page looked like (with the current **_message_** value being set by Javascript on page load):

![](images/Screen_Shot_2014-02-24_at_17_45_03.png)

Next I used the Groovy script below to send a PUT command (I could also had used the [Groovy HttpBuilder](http://groovy.codehaus.org/HTTP+Builder) or the [Java Firebase](https://www.firebase.com/docs/java-api/javadoc/index.html) libraries):

![](images/Screen_Shot_2014-02-24_at_17_45_39.png)

When executed, this script will change the value of the current Firebase app to _"Data from Groovy!!!!"_, which will be shown in real-time (i.e. no browser reload) in the opened test page:

![](images/Screen_Shot_2014-02-24_at_17_45_56.png)

We can also submit (i.e. PUT) name-value pairs:

![](images/Screen_Shot_2014-02-24_at_17_47_03.png)

... which will look like this on the Firebase admin panel:

![](images/Screen_Shot_2014-02-24_at_17_47_13.png)

Next test was to see how to use POST (instead of PUT) on the REST API (in order to replicated the Firebase _push_ command).

To see the result, I changed back the html page to handle items (vs 'a value'), and changed the **_on_** event hook to be **child_added**:

![](images/Screen_Shot_2014-02-24_at_17_49_27.png)

On refresh, this is what the test page looks like:

![](images/Screen_Shot_2014-02-24_at_17_49_38.png)

... and if we send data using POST on the REST call:

![](images/Screen_Shot_2014-02-24_at_17_50_05.png)

... we will get a callback in real-time (again with no browser refresh):

![](images/Screen_Shot_2014-02-24_at_17_50_13.png)

A real cool feature of Firebase is how easy it is to create new **_namespaces_** (or areas/objects) for specific types of data.

For example, if I add _Area51_ to the firebase url (see the highlighted text below)

![](images/Screen_Shot_2014-02-24_at_17_50_55.png)


... the data will now be stored inside an **_Area51_** object/area/namespace on the current Firebase app:

![](images/Screen_Shot_2014-02-24_at_17_51_11.png)

**6) Programatically add new items to the Chat window**  

Finally coming back to the chat window (see below), when I saw that example, one of my first questions was **_"How to programmatically submit data to it?_**

![](images/Screen_Shot_2014-02-24_at_17_53_32.png)

Hopefully by now you should have a clear picture of how to do it, but just in case, here is how I did it :)

For reference, here is what the data looks like:

![](images/Screen_Shot_2014-02-24_at_17_53_53.png)

Here is the script that submits the POST data to this chat (the key is in the **_chat.json_** part of the URL)

![](images/Screen_Shot_2014-02-24_at_17_54_26.png)

And now, after executing the above script, the chat window will contain our new message:

![](images/Screen_Shot_2014-02-24_at_17_54_44.png)
