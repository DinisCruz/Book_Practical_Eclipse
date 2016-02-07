## Using Firebase to sync data with a webpage (via Javascript, REST and Firebase Admin panel)

If you haven't seen the [Anant Narayanan](https://twitter.com/anantn) presentation on [AngularJS conference](http://ng-conf.org/) called [Building realtime apps with Firebase and AngularJS](http://www.youtube.com/watch?v=e4yUTkva_FM) you are missing something good.

[Firebase](https://www.firebase.com/) really seems to fix one of the pain points that I currently have in client-server development, which is _how to send/synchronise data across multiple clients (including the server)_.

I first heard about Firebase from the **_Wire up a Backend_** example that can be found at [http://angularjs.org](http://angularjs.org/), and today I was able to give it a test drive (since I want to use it on the AngularJS front-ends that I'm currently developing for [TeamMentor](https://teammentor.net/))

**1) Creating an Firebase account**  
**  
**Lets start with creating an account and following the [Firebase 5 minute tutorial](https://www.firebase.com/tutorial/).  
**  
**The process of creating an account is just a case of going to [https://firebase.com](https://firebase.com/)

[![](images/Screen_Shot_2014-02-24_at_15_25_53.png)](http://4.bp.blogspot.com/-LRnktMVIrLg/UwuKbH8mCxI/AAAAAAAAHa8/ihJdpm6jQ9Q/s1600/Screen+Shot+2014-02-24+at+15.25.53.png)

... choosing a username and password (there is also the option to create an account based on an GitHub account)

[![](images/Screen_Shot_2014-02-24_at_15_26_22.png)](http://2.bp.blogspot.com/-sBxzFA6DdfY/UwuKbTqz5HI/AAAAAAAAHbM/9ieCZhdv0No/s1600/Screen+Shot+2014-02-24+at+15.26.22.png)

  
... and that's it:

[![](images/Screen_Shot_2014-02-24_at_15_27_11.png)](http://3.bp.blogspot.com/-0y6Mr7_ZkwI/UwuKbViHRGI/AAAAAAAAHbA/HVXexlsJBhc/s1600/Screen+Shot+2014-02-24+at+15.27.11.png)

  
Firebase by default creates a test app, which can be immediately accessed by clicking on the blue _View Firebase _button:

[![](images/Screen_Shot_2014-02-24_at_15_27_40.png)](http://4.bp.blogspot.com/-ku2W7ngcu3w/UwuKb7BSV9I/AAAAAAAAHbI/Y0pn2JS2_I0/s1600/Screen+Shot+2014-02-24+at+15.27.40.png)

**2) Firebase tour**  
**  
**On first load of the Firebase control panel, we are presented with the offer to take a tour, which is a great way to understand the basics of how it works.

[![](images/Screen_Shot_2014-02-24_at_15_27_55.png)](http://1.bp.blogspot.com/-MFi-mQCMOys/UwuKeRQMo2I/AAAAAAAAHb8/HtlHaZTZpng/s1600/Screen+Shot+2014-02-24+at+15.27.55.png)

  
The first step of the tour is to add some data:

[![](images/Screen_Shot_2014-02-24_at_15_28_16.png)](http://1.bp.blogspot.com/-I6BZjQ-4bT8/UwuKcQXhK9I/AAAAAAAAHbg/cjcMvjwiIxA/s1600/Screen+Shot+2014-02-24+at+15.28.16.png)

  
... directly on the current's App data viewer:

[![](images/Screen_Shot_2014-02-24_at_15_28_47.png)](http://1.bp.blogspot.com/-gkneGZnyCQA/UwuKcX5FsYI/AAAAAAAAHbc/4lwUXxv3UWw/s1600/Screen+Shot+2014-02-24+at+15.28.47.png)

  
After we click on the **Add **button, we will see that our data is now part of this Firebase App data stream:

[![](images/Screen_Shot_2014-02-24_at_15_29_05.png)](http://1.bp.blogspot.com/-6MFLK1XvAVY/UwuKdemIHJI/AAAAAAAAHbo/uLPlGgE3rlk/s1600/Screen+Shot+2014-02-24+at+15.29.05.png)

  
Next (after clicking on the **See it in action **link), we get this mini chat application with 3 messages:

[![](images/Screen_Shot_2014-02-24_at_15_29_37.png)](http://3.bp.blogspot.com/-3wTWSpC-TsA/UwuKdmU6zhI/AAAAAAAAHbw/bUO7SWLAtx8/s1600/Screen+Shot+2014-02-24+at+15.29.37.png)

  


If we add a new message:

[![](images/Screen_Shot_2014-02-24_at_15_29_57.png)](http://2.bp.blogspot.com/-5BBoDSEHcig/UwuKd9MsUVI/AAAAAAAAHcE/QutN3OQPjXo/s1600/Screen+Shot+2014-02-24+at+15.29.57.png)

  
... and look back to the Firebase admin panel, we will see the 4 messages (3 added by the **_Sample Chat Application_** and the one I added manually)

[![](images/Screen_Shot_2014-02-24_at_15_30_12.png)](http://2.bp.blogspot.com/-zh4cZmx9cgI/UwuKev42SDI/AAAAAAAAHcA/10d2nStg-BM/s1600/Screen+Shot+2014-02-24+at+15.30.12.png)

  
The final step of the tour is to make a change directly on the Firebase admin panel:

[![](images/Screen_Shot_2014-02-24_at_15_30_29.png)](http://3.bp.blogspot.com/-asG-xcT-2wI/UwuKhUV8qEI/AAAAAAAAHdA/TSwIj1GAJvo/s1600/Screen+Shot+2014-02-24+at+15.30.29.png)

  
... and confirm that the value was _automagically _changed in the **_Sample Chat Application_** (in real-time with no user interaction)

[![](images/Screen_Shot_2014-02-24_at_15_30_48.png)](http://2.bp.blogspot.com/-VaMl_S9I-h8/UwuKfODh3uI/AAAAAAAAHcY/NcQmPR41Q3Q/s1600/Screen+Shot+2014-02-24+at+15.30.48.png)

**3) Creating a simple Html/Javascript page to test it out**  
**  
**Note: The next set of example will use code snippets provided by the Firebase [Web Quickstart Guide](https://www.firebase.com/docs/web-quickstart.html)

[![](images/Screen_Shot_2014-02-24_at_15_37_22.png)](http://3.bp.blogspot.com/-Z7Hb4tNXzkQ/UwuKfdpPj0I/AAAAAAAAHcU/d-2yRDoSG-o/s1600/Screen+Shot+2014-02-24+at+15.37.22.png)

  
Since I'm going to use Eclipse (Kepler), the first step is to create a new **_Static Web Project_**

[![](images/Screen_Shot_2014-02-24_at_15_38_06.png)](http://4.bp.blogspot.com/-0K5f5uLdSwk/UwuKf1-ltYI/AAAAAAAAHcc/xsMFPeGHCho/s1600/Screen+Shot+2014-02-24+at+15.38.06.png)

  
... with a simple HTML inside:

[![](images/Screen_Shot_2014-02-24_at_15_38_54.png)](http://4.bp.blogspot.com/-V-9fobzVR0U/UwuKgAQbZSI/AAAAAAAAHcw/rDkxq10nkn0/s1600/Screen+Shot+2014-02-24+at+15.38.54.png)

  


... containing the just the **_firebase.js _**script import and a simple data setter:

[![](images/Screen_Shot_2014-02-24_at_15_43_26.png)](http://1.bp.blogspot.com/-uRqzqnAQURM/UwuKgzyh04I/AAAAAAAAHc4/vDuWY-yqI3Q/s1600/Screen+Shot+2014-02-24+at+15.43.26.png)

  
To see this in action inside Eclipse, I opened up the admin Url in a Browser window (I wonder how long until an Eclipse Firebase plugin is created), and I logged in:

[![](images/Screen_Shot_2014-02-24_at_15_43_51.png)](http://4.bp.blogspot.com/-ehtKPqHMs1E/UwuKjsdU1qI/AAAAAAAAHds/aNDTqKJ3x20/s1600/Screen+Shot+2014-02-24+at+15.43.51.png)

  
**  
****4) Setting and Pushing data**  
**  
**At this stage I had the Html at the top and the Firebase admin panel at the bottom (note the required full url in the **_var myRootRefnew Firebase(...)_** Javascript code):

[![](images/Screen_Shot_2014-02-24_at_15_46_22.png)](http://1.bp.blogspot.com/-MwCFtxz_fbg/UwuKiUcevOI/AAAAAAAAHdc/e3KY6PJGIqQ/s1600/Screen+Shot+2014-02-24+at+15.46.22.png)

  
Next step was to open a Web Browser with the test page:

[![](images/Screen_Shot_2014-02-24_at_15_44_23.png)](http://3.bp.blogspot.com/-Scj9On_Mqbg/UwuKh_tc-FI/AAAAAAAAHdQ/JVKqRwfwSTM/s1600/Screen+Shot+2014-02-24+at+15.44.23.png)

  


  


  


... which set the Firebase server side value to "Hello World!" (I have to say it made me a bit nervous to see how easy it was to completely remove an entire Firebase dataset (I wonder if there are backup or transaction logs for Firebase data))

[![](images/Screen_Shot_2014-02-24_at_15_46_40.png)](http://2.bp.blogspot.com/-ekBHP-rFrSs/UwuKi7oNA8I/AAAAAAAAHdg/I3lIpt0JShE/s1600/Screen+Shot+2014-02-24+at+15.46.40.png)

  
Next step was to try setting some name-value pairs (i.e. a typical JSON string):

[![](images/Screen_Shot_2014-02-24_at_15_51_46.png)](http://2.bp.blogspot.com/-4YBno-rW2_8/UwuKjN4EP9I/AAAAAAAAHdo/-sUnlPmMh7I/s1600/Screen+Shot+2014-02-24+at+15.51.46.png)

  
... which looked like this after execution (note that I didn't refresh the Firebase admin panel (it also uses the WebSocket technology to keep itself up-to-date))

[![](images/Screen_Shot_2014-02-24_at_15_51_55.png)](http://3.bp.blogspot.com/-JriOUL-NirU/UwuKjtdzXkI/AAAAAAAAHeE/S8OpWL8NiIc/s1600/Screen+Shot+2014-02-24+at+15.51.55.png)

  
Next I tried the **_push_** method (which behaves like an array and was the technique used in the chat example):

[![](images/Screen_Shot_2014-02-24_at_15_54_41.png)](http://1.bp.blogspot.com/-jvwa6PXw2Lw/UwuKj8oqwgI/AAAAAAAAHeA/wbKdXDYctpE/s1600/Screen+Shot+2014-02-24+at+15.54.41.png)

  
Here is the execution result (note how there is now an extra **_TreeNode_** with the data provided)

[![](images/Screen_Shot_2014-02-24_at_15_55_01.png)](http://4.bp.blogspot.com/-Gp1peAmFcYI/UwuKkMlX2eI/AAAAAAAAHd8/gSKm_4CxS2U/s1600/Screen+Shot+2014-02-24+at+15.55.01.png)

**5) receiving events**  
**  
**So far we have been setting/pushing data into Firebase, but what is also really powerful, is that we can subscribe to server-side events, and update the browser/ui when content changes.

The example below shows how to get a callback every-time a new item is added:

[![](images/Screen_Shot_2014-02-24_at_16_02_46.png)](http://3.bp.blogspot.com/-V4jQUhLEXPw/UwuKk38hG6I/AAAAAAAAHec/8ZOyuR55Dfk/s1600/Screen+Shot+2014-02-24+at+16.02.46.png)

  
Now on refresh (screenshot below), the new children will be shown on the page:

[![](images/Screen_Shot_2014-02-24_at_16_03_02.png)](http://2.bp.blogspot.com/-nsY97HBYo8g/UwuKk_2wptI/AAAAAAAAHeY/ZQiu-O5iOUo/s1600/Screen+Shot+2014-02-24+at+16.03.02.png)

  
One observation, when we subscribe to the _child_added _event,_ _any changes made directly in Firebase's admin panel:

[![](images/Screen_Shot_2014-02-24_at_16_03_31.png)](http://3.bp.blogspot.com/-Fj9VoHQ-d6k/UwuKlPT4oUI/AAAAAAAAHeU/hSQmVqL8uAM/s1600/Screen+Shot+2014-02-24+at+16.03.31.png)

  
... will only be seen when we refresh the page (where all items are viewed as new children)

[![](images/Screen_Shot_2014-02-24_at_16_03_52.png)](http://1.bp.blogspot.com/-x4xTNojYkMs/UwuKoIQ44XI/AAAAAAAAHfU/7t9DQA_fRNE/s1600/Screen+Shot+2014-02-24+at+16.03.52.png)

  
To see the changes in real-time, we need to change the event to _child_changed :_

[![](images/Screen_Shot_2014-02-24_at_16_11_22.png)](http://2.bp.blogspot.com/-FG9fwQPi0Zw/UwuKmICeZPI/AAAAAAAAHes/WEiERRilyGM/s1600/Screen+Shot+2014-02-24+at+16.11.22.png)

  
Now (on refresh) we get an empty list:

[![](images/Screen_Shot_2014-02-24_at_16_11_31.png)](http://4.bp.blogspot.com/-xxspj5XYxvI/UwuKm22OtMI/AAAAAAAAHe0/Ozdx90-4l9c/s1600/Screen+Shot+2014-02-24+at+16.11.31.png)

  
... but if the content is changed on the Firebase admin panel:

[![](images/Screen_Shot_2014-02-24_at_16_11_58.png)](http://3.bp.blogspot.com/-QjB42k5HO_M/UwuKnPNB2UI/AAAAAAAAHfE/3crHz9dGJfU/s1600/Screen+Shot+2014-02-24+at+16.11.58.png)

  
... the _child_changed_ event is triggered, and we will the new content changes on the browser (without page reload)

[![](images/Screen_Shot_2014-02-24_at_16_12_09.png)](http://1.bp.blogspot.com/-KjvJEQEzxNI/UwuKnWm5vvI/AAAAAAAAHfI/IeEzUD13dus/s1600/Screen+Shot+2014-02-24+at+16.12.09.png)

**5) Consuming and Sending events using REST API**  
**  
**Now that we can create and consume Firebase events using Javascript, it is time to try their REST API.

For that, I'm going to use the [Eclipse Grovy REPL Scripting Environment 1.6.0](http://marketplace.eclipse.org/content/eclipse-grovy-repl-scripting-environment) so that I can do it directly from Eclipse

Note: most scripts shown below are on [this gist](https://gist.github.com/DinisCruz-Dev/9193091)

The first test was to get the current data set, which is easily retrieved via a simple GET request to the Firebase url for the current application (with a **.json **appended to in the end of the admin url):

[![](images/Screen_Shot_2014-02-24_at_16_28_28.png)](http://4.bp.blogspot.com/-xPFtammESXo/UwuKoAHdOtI/AAAAAAAAHfY/zNOKq30fr8k/s1600/Screen+Shot+2014-02-24+at+16.28.28.png)

  
Since we are in eclipse, here is the code to open the **_JavaScript Editor_** programatically with the json data received:

[![](images/Screen_Shot_2014-02-24_at_16_28_58.png)](http://2.bp.blogspot.com/-nbwVowJix8g/UwuKpAUkmWI/AAAAAAAAHfw/D06ZSkWCwjU/s1600/Screen+Shot+2014-02-24+at+16.28.58.png)

  
By default the data received from the server has no formatting:  


  


[![](images/Screen_Shot_2014-02-24_at_16_29_08.png)](http://2.bp.blogspot.com/-FyPhbgRTjMg/UwuKo7S9ixI/AAAAAAAAHfg/9_IGeYU_NlY/s1600/Screen+Shot+2014-02-24+at+16.29.08.png)

  
But since we are inside the Eclipse  **_JavaScript Editor_**  if we assign it to a variable, we can easily format it:

[![](images/Screen_Shot_2014-02-24_at_16_29_32.png)](http://4.bp.blogspot.com/-zmZwwRmTtx0/UwuKrkN2aZI/AAAAAAAAHgY/oUFf7e-ksS4/s1600/Screen+Shot+2014-02-24+at+16.29.32.png)

  
After doing this, I discovered that if we pass a _?print=pretty _to the Firebase url:

[![](images/Screen_Shot_2014-02-24_at_16_32_40.png)](http://3.bp.blogspot.com/-I_7D8_OsoqQ/UwuKpXT1YGI/AAAAAAAAHfs/9inJuLzge5I/s1600/Screen+Shot+2014-02-24+at+16.32.40.png)

  
... the received json data will already be nicely formatted:

[![](images/Screen_Shot_2014-02-24_at_16_32_46.png)](http://3.bp.blogspot.com/-1OcOadZtIGc/UwuKp03IMLI/AAAAAAAAHf4/9S5Lm-nJj6I/s1600/Screen+Shot+2014-02-24+at+16.32.46.png)

  
In the example below I used the Groovy REPL _Execution result_ window to see the formatted json data:

[![](images/Screen_Shot_2014-02-24_at_16_36_51.png)](http://1.bp.blogspot.com/-Fb70_Z7GFzU/UwuKqB14fFI/AAAAAAAAHf8/jAlaQqPg9FA/s1600/Screen+Shot+2014-02-24+at+16.36.51.png)

  
Next thing I wanted to try was to see how a REST change would be shown in real time in the browser.

Because my next REST request will use the HTTP PUT command (which is equivalent to the Firebase **_set_** Javascript function), I changed the Html page to display and listen for Firebase _values _(vs arrays with name-value pairs)

Note the **_snapshot.valueOf().val() _**command below:

[![](images/Screen_Shot_2014-02-24_at_17_44_32.png)](http://2.bp.blogspot.com/-TLKn9uBNNr4/UwuKs65fwHI/AAAAAAAAHg0/k4nY_sGEAaI/s1600/Screen+Shot+2014-02-24+at+17.44.32.png)

  


After browser refresh, this is what the test page looked like (with the current **_message_** value being set by Javascript on page load):

[![](images/Screen_Shot_2014-02-24_at_17_45_03.png)](http://2.bp.blogspot.com/-qSLM3z47JOU/UwuKrN3aV9I/AAAAAAAAHgQ/xpuc2aWt5qI/s1600/Screen+Shot+2014-02-24+at+17.45.03.png)

  
Next I used the Groovy script below to send a PUT command (I could also had used the [Groovy HttpBuilder](http://groovy.codehaus.org/HTTP+Builder) or the [Java Firebase](https://www.firebase.com/docs/java-api/javadoc/index.html) libraries):

[![](images/Screen_Shot_2014-02-24_at_17_45_39.png)](http://2.bp.blogspot.com/-bhE0RYWCSk8/UwuKrqIZ7nI/AAAAAAAAHgo/hvTTQs1W2J4/s1600/Screen+Shot+2014-02-24+at+17.45.39.png)

  
When executed, this script will change the value of the current Firebase app to _"Data from Groovy!!!!"_, which will be shown in real-time (i.e. no browser reload) in the opened test page:

[![](images/Screen_Shot_2014-02-24_at_17_45_56.png)](http://3.bp.blogspot.com/-J0-vhth4yLE/UwuKr681AQI/AAAAAAAAHgk/hqZnLMHog3I/s1600/Screen+Shot+2014-02-24+at+17.45.56.png)

  
We can also submit (i.e. PUT) name-value pairs:

[![](images/Screen_Shot_2014-02-24_at_17_47_03.png)](http://2.bp.blogspot.com/-fwb_-UFILL4/UwuKysoVeLI/AAAAAAAAHik/Qxswjrks1rY/s1600/Screen+Shot+2014-02-24+at+17.47.03.png)

  
... which will look like this on the Firebase admin panel:

[![](images/Screen_Shot_2014-02-24_at_17_47_13.png)](http://4.bp.blogspot.com/-LZjTR_aQY9E/UwuKs-FFrgI/AAAAAAAAHg4/a-J01xzlWIw/s1600/Screen+Shot+2014-02-24+at+17.47.13.png)

Next test was to see how to use POST (instead of PUT) on the REST API (in order to replicated the Firebase _push _command).

To see the result, I changed back the html page to handle items (vs 'a value'), and changed the **_on_** event hook to be **child_added**:

[![](images/Screen_Shot_2014-02-24_at_17_49_27.png)](http://2.bp.blogspot.com/-LKj57BzXIb0/UwuKtpzO6mI/AAAAAAAAHhA/uWvRZZdkhVM/s1600/Screen+Shot+2014-02-24+at+17.49.27.png)

  
On refresh, this is what the test page looks like:

[![](images/Screen_Shot_2014-02-24_at_17_49_38.png)](http://4.bp.blogspot.com/-gLobHN8Ha90/UwuKuJw9-CI/AAAAAAAAHhQ/ATQiuXnDWjg/s1600/Screen+Shot+2014-02-24+at+17.49.38.png)

  
... and if we send data using POST on the REST call:

[![](images/Screen_Shot_2014-02-24_at_17_50_05.png)](http://3.bp.blogspot.com/-3207-fTtkNg/UwuKumFcoSI/AAAAAAAAHhY/kuJeg5DAfFQ/s1600/Screen+Shot+2014-02-24+at+17.50.05.png)

  
... we will get a callback in real-time (again with no browser refresh):

[![](images/Screen_Shot_2014-02-24_at_17_50_13.png)](http://4.bp.blogspot.com/-PNR8EVZgRk0/UwuKu4Cr_2I/AAAAAAAAHhg/iq13l8o8BD8/s1600/Screen+Shot+2014-02-24+at+17.50.13.png)

A real cool feature of Firebase is how easy it is to create new **_namespaces_** (or areas/objects) for specific types of data.

For example, if I add _Area51 _to the firebase url (see the highlighted text below)

[![](images/Screen_Shot_2014-02-24_at_17_50_55.png)](http://4.bp.blogspot.com/-sD7jqZFlfY8/UwuKvEKT5iI/AAAAAAAAHho/BuP3FqHb0NA/s1600/Screen+Shot+2014-02-24+at+17.50.55.png)

  
... the data will now be stored inside an **_Area51_** object/area/namespace on the current Firebase app:

[![](images/Screen_Shot_2014-02-24_at_17_51_11.png)](http://1.bp.blogspot.com/-nPN4gtk5cIE/UwuKvhdviLI/AAAAAAAAHhw/G7mkmFCfj0M/s1600/Screen+Shot+2014-02-24+at+17.51.11.png)

**6) Programatically add new items to the Chat window**  
**  
**Finally coming back to the chat window (see below), when I saw that example, one of my first questions was **_"How to programmatically submit data to it?_**

[![](images/Screen_Shot_2014-02-24_at_17_53_32.png)](http://4.bp.blogspot.com/-HE-wkzEw0mk/UwuKv-epDrI/AAAAAAAAHh4/RnBiknIaczA/s1600/Screen+Shot+2014-02-24+at+17.53.32.png)

  
Hopefully by now you should have a clear picture of how to do it, but just in case, here is how I did it :)

For reference, here is what the data looks like:

[![](images/Screen_Shot_2014-02-24_at_17_53_53.png)](http://2.bp.blogspot.com/-btbeGFzDbK8/UwuKwXg3nTI/AAAAAAAAHiA/69l8AdLq_2c/s1600/Screen+Shot+2014-02-24+at+17.53.53.png)

  


Here is the script that submits the POST data to this chat (the key is in the **_chat.json_** part of the URL)

[![](images/Screen_Shot_2014-02-24_at_17_54_26.png)](http://4.bp.blogspot.com/-JYVWnmyzvtU/UwuKxO5s7WI/AAAAAAAAHiM/XwWHnHXyaSM/s1600/Screen+Shot+2014-02-24+at+17.54.26.png)

  
And now, after executing the above script, the chat window will contain our new message:

[![](images/Screen_Shot_2014-02-24_at_17_54_44.png)](http://3.bp.blogspot.com/-EpYy55EmJf0/UwuKxvr0jWI/AAAAAAAAHiY/PCB6ptL6x3E/s1600/Screen+Shot+2014-02-24+at+17.54.44.png)

  


  


**6) What about XSS**  
**  
**Although both **_chat_** application and test html page are not vulnerable to XSS, it is very easy to create an DOM based XSS in this type of real-time apps.

See my next post on [XSS considerations when developing with Firebase](http://blog.diniscruz.com/2014/02/xss-considerations-when-developing-with.html) for more details on this topic. 
