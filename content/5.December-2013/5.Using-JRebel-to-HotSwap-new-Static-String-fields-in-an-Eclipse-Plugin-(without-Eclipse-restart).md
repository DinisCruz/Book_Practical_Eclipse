## Using JRebel to HotSwap new Static String fields in an Eclipse Plugin (without Eclipse restart)

After [Installing, compiling and failing to use DCE VM for Eclipse Plugin development](http://blog.diniscruz.com/2013/12/installing-compiling-and-failing-to-use.html) it was time to give [JRebel](http://zeroturnaround.com/software/jrebel/) a go (which is a commercial plugin that costs about ~300 USD per year).

TLDR: It worked and I was able to run an Eclipse Plugin, make big changes in a class already loaded (like adding a new field/method), and have access to those changes without needing to restart Eclipse.

**Part 1: Installing JRebel**

First step was to install JRebel from the Eclipse Marketplace:

[![](images/Screen_Shot_2013-12-16_at_04_24_01.png)](http://1.bp.blogspot.com/-l_nHmoP6UlA/Uq8r5dfDlUI/AAAAAAAAFIA/kICxth1UALo/s1600/Screen+Shot+2013-12-16+at+04.24.01.png)

  


 ... with these features:

[![](images/Screen_Shot_2013-12-16_at_04_24_14.png)](http://2.bp.blogspot.com/-d1Ykp8SxcHE/Uq8r5SxElQI/AAAAAAAAFH8/njTVVkNaXmU/s1600/Screen+Shot+2013-12-16+at+04.24.14.png)

  
... which took a little bit to install since there were a number of large downloads:

[![](images/Screen_Shot_2013-12-16_at_04_24_56.png)](http://3.bp.blogspot.com/-C4z1UaSlYTA/Uq8r5blb6_I/AAAAAAAAFH4/-JAcLrCA338/s1600/Screen+Shot+2013-12-16+at+04.24.56.png)

  


After the installation (and Eclipse restart) we get an alert message that looks like this:

  


[![](images/Screen_Shot_2013-12-16_at_04_40_05.png)](http://4.bp.blogspot.com/-pHajDvqD0nY/Uq8r6LCODII/AAAAAAAAFII/gY6NeAo4sZE/s1600/Screen+Shot+2013-12-16+at+04.40.05.png)

  


Clicking on the **_Active your license_** takes us to this screen:

[![](images/Screen_Shot_2013-12-16_at_04_40_39.png)](http://2.bp.blogspot.com/-R5s22u30v2k/Uq8r6QgLqYI/AAAAAAAAFIg/sMOP3-6wQIY/s1600/Screen+Shot+2013-12-16+at+04.40.39.png)

  


Clicking on the **_Evaluate_** takes us to the JRebel website where we can request a license:

[![](images/Screen_Shot_2013-12-16_at_04_41_19.png)](http://1.bp.blogspot.com/-11ZmEUXePk4/Uq8r6T7dypI/AAAAAAAAFIc/Sr8TeaI4uOE/s1600/Screen+Shot+2013-12-16+at+04.41.19.png)

  


 ... which is sent immediately (thx [Zero Turnaround](http://zeroturnaround.com/)):

[![](images/Screen_Shot_2013-12-16_at_04_41_58.png)](http://3.bp.blogspot.com/-vGggRZbJ_K0/Uq8r6jJQKpI/AAAAAAAAFIY/4iWVtPUFKr8/s1600/Screen+Shot+2013-12-16+at+04.41.58.png)

  
To activate it, I copied and paste the license string (without the pre and post comments) into the provided TextBox , and we get a little visual clue (top left icon goes green) that the license is good:

[![](images/Screen_Shot_2013-12-16_at_04_43_02.png)](http://4.bp.blogspot.com/-6hSIi_Yj2t4/Uq8r7QRkgfI/AAAAAAAAFI8/juk8yQVS7yY/s1600/Screen+Shot+2013-12-16+at+04.43.02.png)

  
**  
****Part 2: Configure JRebel**  
**  
**To add JRebel to the Plugin project, there were two things to do:

1) add the JRebel Nature:

[![](images/Screen_Shot_2013-12-16_at_04_43_31.png)](http://4.bp.blogspot.com/-rN7lXGPfKhA/Uq8r7tRpPuI/AAAAAAAAFI0/XcWxSj3l-wI/s1600/Screen+Shot+2013-12-16+at+04.43.31.png)

  
2) enable JRebel in the desired Run Configuration:

[![](images/Screen_Shot_2013-12-16_at_04_49_32.png)](http://3.bp.blogspot.com/-OJgIw5VdAuQ/Uq8r7gxdKGI/AAAAAAAAFIs/xVXpNg9SkWk/s1600/Screen+Shot+2013-12-16+at+04.49.32.png)

  


  


Once that was done, I started the eclipse plugin (under **_Run_** not **_Debug_**)

[![](images/Screen_Shot_2013-12-16_at_16_45_07.png)](http://4.bp.blogspot.com/-vIppr8rV59A/Uq8vkhg1hAI/AAAAAAAAFJQ/kJmS3VKtN-Y/s1600/Screen+Shot+2013-12-16+at+16.45.07.png)

  
Note: there was this message which can be ignored (for now) since I'm not going to use an Java Project or server in this test/PoC

[![](images/Screen_Shot_2013-12-16_at_16_45_40.png)](http://2.bp.blogspot.com/-SyU0ciXmW1E/Uq8vkm3PoMI/AAAAAAAAFJM/pVuiLMWUdfw/s1600/Screen+Shot+2013-12-16+at+16.45.40.png)

**Part 3: Using JRebel to add new fields and methods**  
**  
**With JRebel enabled in the spawned Eclipse instance (the one that loads the [TeamMentor](https://teammentor.net/) Plugin from class files and not a jar), I opened the **_Write TeamMentor Script_** UI  and wrote a simple groovy script that showed the contents of a static String from the **_tm.utils.Consts_Eclipse_** class.

In the screenshot below, the top part (with the java code files) belongs to the host eclipse instance, and the bottom part is the TeamMentor Groovy based Script editor running on the spawned Eclipse instance.

[![](images/Screen_Shot_2013-12-16_at_16_47_35.png)](http://4.bp.blogspot.com/-ipYWGHQDQKY/Uq8vlOMFjUI/AAAAAAAAFKE/rVs0A8npp9Q/s1600/Screen+Shot+2013-12-16+at+16.47.35.png)

The script above showed how we can write a groovy script that gets the a static value from a class, and the script below shows how to get a list of fields from that class (which at the moment is 3)  


  


  


[![](images/Screen_Shot_2013-12-16_at_16_48_36.png)](http://4.bp.blogspot.com/-sxIvkU_FqHM/Uq8vlBKnsUI/AAAAAAAAFJo/ptr-tvWZqvE/s1600/Screen+Shot+2013-12-16+at+16.48.36.png)

  


  


The first test I want to do (which is the one that doesn't work with the current JVM HotSwap) is to add a new static field to that **_Consts_Eclipse_** class, and have access to it, **without needing to restart Eclipse!**

And that is exactly what you can see in the screenshot below :)

Note how there is a new static String field on the top editor (called **TEST_NEW**), which is then listed by the groovy script below:

[![](images/Screen_Shot_2013-12-16_at_16_49_28.png)](http://1.bp.blogspot.com/-OivvlVv6TV0/Uq8vlZbmJjI/AAAAAAAAFJg/tvsO-x_8F5U/s1600/Screen+Shot+2013-12-16+at+16.49.28.png)

  
A quick glance at the Console view, will also show JRebel in action:

[![](images/Screen_Shot_2013-12-16_at_16_49_51.png)](http://2.bp.blogspot.com/-sPTt_r8t5uE/Uq8vlzZFSLI/AAAAAAAAFJs/QUAUAFyNOeI/s1600/Screen+Shot+2013-12-16+at+16.49.51.png)

  
We can use the same technique to have access to its value:  


  


[![](images/Screen_Shot_2013-12-16_at_16_50_11.png)](http://3.bp.blogspot.com/-HfBKE7PMc7M/Uq8vmEY6aFI/AAAAAAAAFKA/12t4e8GpLVw/s1600/Screen+Shot+2013-12-16+at+16.50.11.png)

  
Here is what happens if we try to access a field that doesn't (yet) exist:

[![](images/Screen_Shot_2013-12-16_at_16_50_28.png)](http://1.bp.blogspot.com/-wc1V5m67awo/Uq8vmTuA0PI/AAAAAAAAFJ8/RW0gaAdZnos/s1600/Screen+Shot+2013-12-16+at+16.50.28.png)

  
And here is what happens when that 'non existent' field is added:

[![](images/Screen_Shot_2013-12-16_at_16_50_50.png)](http://2.bp.blogspot.com/-nQ4Ug4xewns/Uq8vnGa9dBI/AAAAAAAAFKQ/3LC95znxzFg/s1600/Screen+Shot+2013-12-16+at+16.50.50.png)

  


Finally I wanted to see if new methods (instance and static) were correctly handled (since this is the use-case that I need from this technology/technique), and it worked like a charm :)

Note how in the example below, two new methods are added to the **_Consts_Eclipse_** class, which are then used (without Eclipse restart) by the groovy script running on the spawned Eclipse instance:

[![](images/Screen_Shot_2013-12-16_at_17_33_06.png)](http://2.bp.blogspot.com/-yNjt6bnGvfw/Uq8520n8GQI/AAAAAAAAFKk/sYEO24WArFY/s1600/Screen+Shot+2013-12-16+at+17.33.06.png)

  
This is REALLY powerful, since I can now work on the Eclipse core APIs (consumed by the TeamMentor plug-in) without needing to restart Eclipse. 
