## Installing, compiling and failing to use DCE VM for Eclipse Plugin development

Last night I tried to use the amazing [DCE VM](http://ssw.jku.at/dcevm/) tool (DCE = Dynamic Code Evolution) to apply hot fixes to the APIs I was creating for the open source [Eclipse API Tool Kit I'm working](http://blog.diniscruz.com/2013/11/si-open-sources-eclipse-plugin.html) on (as part of the [TeamMentor Eclipse](http://blog.diniscruz.com/2013/11/teammentor-plugin-and-builder-v156.html) [Fortify Plugin](http://blog.diniscruz.com/2013/09/two-videos-showing-teammentor-eclipse.html)).

I was trying to address the limitations of the JVM's HotSwap technology which only works on certain inline code changes, and doesn't support at all the addition and changing of new methods.

TLDR: this post **doesn't have the solution for this problem** (see next post which shows JRebel in action).

In this post I'm going to show the workflow/steps that I followed to:

  * create a version of DCE VM that worked on OSX Mavericks (after failing to use the provided binaries, and needing to compile the DCE VM code),  
  * run eclipse under the modified/patched JDK 
  * get a 'hang' in Eclipse when one of the dynamic code changes was applied.

  
  
**Part 1: Trying to install the binaries**  
**  
**The first step was to go to the [DCE VM](http://ssw.jku.at/dcevm/) website:  


  


[![](images/Screen_Shot_2013-12-16_at_15_17_11.png)](http://1.bp.blogspot.com/-GMpSZZd5kyQ/Uq8bwRfUPqI/AAAAAAAAFCo/G-8aO1GRclk/s1600/Screen+Shot+2013-12-16+at+15.17.11.png)

  


Open the [Binaries](http://ssw.jku.at/dcevm/binaries/) page, download the osx version of [dcevm-0.2-mac.jar](http://ssw.jku.at/dcevm/downloads/dcevm-0.2-mac.jar) and execute it locally:

  


[![](images/Screen_Shot_2013-12-16_at_01_58_04.png)](http://2.bp.blogspot.com/-5x8KBp9GO90/Uq8b6s0gY8I/AAAAAAAAFC4/0BzoJfgskj4/s1600/Screen+Shot+2013-12-16+at+01.58.04.png)

  


Unfortunately there were no VMs picked up by default.

So I tried to the the default OSx Java install dir,  which was here:

[![](images/Screen_Shot_2013-12-16_at_02_03_40.png)](http://4.bp.blogspot.com/-0RQeDkctiUQ/Uq8b6uprrCI/AAAAAAAAFC0/82zim41Gpmo/s1600/Screen+Shot+2013-12-16+at+02.03.40.png)

  
But that didn't work:

[![](images/Screen_Shot_2013-12-16_at_02_04_14.png)](http://4.bp.blogspot.com/-zicYnBxhZ7c/Uq8b6lv-qcI/AAAAAAAAFCw/ARMJPBQg3UI/s1600/Screen+Shot+2013-12-16+at+02.04.14.png)

  
So I downloaded from Oracle the latest version of the OSX JDK to this dev laptop:

[![](images/Screen_Shot_2013-12-16_at_02_08_36.png)](http://1.bp.blogspot.com/-7aIx6fQLFHY/Uq8b9-JegwI/AAAAAAAAFD8/Ytv1afUmw98/s1600/Screen+Shot+2013-12-16+at+02.08.36.png)

  


... which was placed here:

[![](images/Screen_Shot_2013-12-16_at_02_12_58.png)](http://2.bp.blogspot.com/-b-SLaEsLYlk/Uq8b7BbMHPI/AAAAAAAAFDM/_47zY3BVmHc/s1600/Screen+Shot+2013-12-16+at+02.12.58.png)

  
But that folder didn't work either

[![](images/Screen_Shot_2013-12-16_at_02_13_12.png)](http://3.bp.blogspot.com/-iJPmc3_-5hs/Uq8b7XMl8RI/AAAAAAAAFDE/oqX57slC2E0/s1600/Screen+Shot+2013-12-16+at+02.13.12.png)

  
So didn't this one:

[![](images/Screen_Shot_2013-12-16_at_02_13_40.png)](http://2.bp.blogspot.com/-JEqb9R51bH4/Uq8b7w2Y2AI/AAAAAAAAFDU/vnsphFfDQQ0/s1600/Screen+Shot+2013-12-16+at+02.13.40.png)

  


[![](images/Screen_Shot_2013-12-16_at_02_13_50.png)](http://4.bp.blogspot.com/-o-QCa6HmvK4/Uq8b8KwFkHI/AAAAAAAAFDY/HCVHayXme3w/s1600/Screen+Shot+2013-12-16+at+02.13.50.png)

  
But this did:

[![](images/Screen_Shot_2013-12-16_at_02_14_34.png)](http://2.bp.blogspot.com/-kf1tKjhH5R4/Uq8b8lOyI6I/AAAAAAAAFDs/lCSRWlvW2-M/s1600/Screen+Shot+2013-12-16+at+02.14.34.png)

  
Well, it was originally recognised as a JDK, but when I clicked on **_Install_**

[![](images/Screen_Shot_2013-12-16_at_02_14_59.png)](http://2.bp.blogspot.com/-OA9_ZUU1gsU/Uq8b8oHV2fI/AAAAAAAAFDk/xnCyOAfu3ow/s1600/Screen+Shot+2013-12-16+at+02.14.59.png)

  
I got this error:

[![](images/Screen_Shot_2013-12-16_at_02_15_14.png)](http://4.bp.blogspot.com/-USWNi0y5nvo/Uq8b9cpafpI/AAAAAAAAFEA/0q0aEWfIfzk/s1600/Screen+Shot+2013-12-16+at+02.15.14.png)

  
**  
****Part 2: Building DCE VM from Source**

Since the binaries option didn't work, it was time for plan B, which was to use the latest version of the code (from GitHub) and build it.

The best instructions I found came from this blog entry from Sogety: [TRUE HOT SWAP IN JAVA WITH DCEVM ON OS-X](http://java.sogeti.nl/JavaBlog/2013/12/09/true-hot-swap-in-java-with-dcevm-on-os-x/) :

[![](images/Screen_Shot_2013-12-16_at_15_37_29.png)](http://2.bp.blogspot.com/-h77SDrsjUn8/Uq8eTTFRlxI/AAAAAAAAFHc/kzAR2tB5Cgk/s1600/Screen+Shot+2013-12-16+at+15.37.29.png)

  
... which took me though the following steps (you can copy and paste the [instructions from that blog post](http://java.sogeti.nl/JavaBlog/2013/12/09/true-hot-swap-in-java-with-dcevm-on-os-x/))

After [installing Gradle](http://blog.diniscruz.com/2013/12/installing-gradle-on-osx.html) and the OSX dev tools, I cloned the [https://github.com/Guidewire/DCEVM](https://github.com/Guidewire/DCEVM) repo and switched into the **_full-jdk7u45_** branch

[![](images/Screen_Shot_2013-12-16_at_03_03_14.png)](http://4.bp.blogspot.com/-tJD_-FSvDj8/Uq8b9liVQiI/AAAAAAAAFD4/cLM7X-5p92g/s1600/Screen+Shot+2013-12-16+at+03.03.14.png)

  
Then I executed **_gradle_**

[![](images/Screen_Shot_2013-12-16_at_03_05_19.png)](http://3.bp.blogspot.com/-9iyhl-D6_vY/Uq8b-eEbL8I/AAAAAAAAFEU/WP31dM913dc/s1600/Screen+Shot+2013-12-16+at+03.05.19.png)

  
.... which took a while (with tons and tons of warning messages)

... and eventually:

[![](images/Screen_Shot_2013-12-16_at_03_18_37.png)](http://4.bp.blogspot.com/-2SSwFHg4hbY/Uq8b-jcSMUI/AAAAAAAAFEQ/IrJrxobVtEY/s1600/Screen+Shot+2013-12-16+at+03.18.37.png)

  
... the compilation completed:

[![](images/Screen_Shot_2013-12-16_at_03_18_47.png)](http://2.bp.blogspot.com/-NBQZuOTJvz8/Uq8b_dhIeMI/AAAAAAAAFFI/UwkE9nYnRmU/s1600/Screen+Shot+2013-12-16+at+03.18.47.png)

  
... the final step was to create a copy of the **_jdk1.7.0_45.jdk _**folder and copy the created *.dylib files into the new _jdk1.7.0_45_dcevm.jdk/Contents/Home/jre/lib/server _folder:

[![](images/Screen_Shot_2013-12-16_at_03_22_20.png)](http://3.bp.blogspot.com/-JnJXl0cuJo4/Uq8b_h8kvDI/AAAAAAAAFEs/LY3SolgSIgg/s1600/Screen+Shot+2013-12-16+at+03.22.20.png)

  
Finally I was able to try it, and I got this error (while executing _java --version _(as mentioned on the [blog post](http://java.sogeti.nl/JavaBlog/2013/12/09/true-hot-swap-in-java-with-dcevm-on-os-x/))

[![](images/Screen_Shot_2013-12-16_at_03_22_47.png)](http://3.bp.blogspot.com/-66PGMUqKiLs/Uq8b_5_mNqI/AAAAAAAAFEo/0MR7i74RzmE/s1600/Screen+Shot+2013-12-16+at+03.22.47.png)

  
... which was caused by the fact that the comment that works is **_java -version_** :)

[![](images/Screen_Shot_2013-12-16_at_15_48_36.png)](http://3.bp.blogspot.com/-X8F5wVaAD3Y/Uq8g67-Mq0I/AAAAAAAAFHo/GtPffipovsA/s1600/Screen+Shot+2013-12-16+at+15.48.36.png)

  


So as you can see from the screenshot above, we now have a patched JVM with Dynamic Code Evolution enabled :)

**Step 3) trying to use the patch JVM to run the TeamMentor Eclipse Plugin**  
**  
**Since there are a number of blog posts out there that show that once you have the patched JVM it should work (see  [Dynamic Code Evolution for Java](http://jaxenter.com/dynamic-code-evolution-for-java-37373.html), [Redeploy alternatives to JRebel](http://stackoverflow.com/questions/7998669/redeploy-alternatives-to-jrebel) and  [Get True Hot Swap in Java with DCEVM and IntelliJ IDEA](http://blog.jetbrains.com/idea/2013/07/get-true-hot-swap-in-java-with-dcevm-and-intellij-idea/) ), it was time to see it in action :)

I opened up the Eclipse which has the dev version of the plugin, went into the **_Run Configurations_** page, and created a duplicate of my main **_Eclipse Application_** configuration:

[![](images/Screen_Shot_2013-12-16_at_03_26_29.png)](http://1.bp.blogspot.com/-eg0KltgOMLU/Uq8cAivLNhI/AAAAAAAAFFE/9KvQcqFpzWg/s1600/Screen+Shot+2013-12-16+at+03.26.29.png)

  


Then, on the**_ Java Runtime Environment_** section,  I clicked on the **_Environments_** button:

[![](images/Screen_Shot_2013-12-16_at_03_27_13.png)](http://2.bp.blogspot.com/-UvEaMwaLVI0/Uq8cA3DLBDI/AAAAAAAAFFA/gDLAZXuKyoI/s1600/Screen+Shot+2013-12-16+at+03.27.13.png)

  
Where I had to add the patched 1.7 JDK by clicking on **_Add..._**

[![](images/Screen_Shot_2013-12-16_at_03_27_21.png)](http://4.bp.blogspot.com/-So5bzEgJQgI/Uq8cBa0reqI/AAAAAAAAFFg/mkbd3s_UORY/s1600/Screen+Shot+2013-12-16+at+03.27.21.png)

  
Then choosing **_Standard VM_** on **_Add JRE_** popup window:

[![](images/Screen_Shot_2013-12-16_at_03_27_28.png)](http://4.bp.blogspot.com/-pMDKCw9FqtA/Uq8cBh7kfJI/AAAAAAAAFFc/qhCO1TZXB2E/s1600/Screen+Shot+2013-12-16+at+03.27.28.png)

  


... selected this folder (note the**_ jdk1.7.0_45_dcevm.jdk_** in the path)

[![](images/Screen_Shot_2013-12-16_at_03_28_20.png)](http://4.bp.blogspot.com/-NaOjhW6JB7w/Uq8cBzfh96I/AAAAAAAAFFY/lMb3A2lGq7A/s1600/Screen+Shot+2013-12-16+at+03.28.20.png)

  
... gave it a relevant name (in this case **_JDK 1.7 - DCE VM_**), and clicked clicked on **Finish**:

[![](images/Screen_Shot_2013-12-16_at_03_28_50.png)](http://3.bp.blogspot.com/-d9i_jiZveZk/Uq8cCk0mY_I/AAAAAAAAFF4/Z2hMofGAhHk/s1600/Screen+Shot+2013-12-16+at+03.28.50.png)

  
Next I selected the newly created JDK mapping from the **_Execution Environment_** drop-down:

[![](images/Screen_Shot_2013-12-16_at_03_29_26.png)](http://2.bp.blogspot.com/-nQl0k81CRe4/Uq8cCxYWFII/AAAAAAAAFF0/ehqwvcPJhzA/s1600/Screen+Shot+2013-12-16+at+03.29.26.png)

  
And clicked on **Run**

[![](images/Screen_Shot_2013-12-16_at_03_29_50.png)](http://2.bp.blogspot.com/-UwtvTRZ9aE4/Uq8cD1yponI/AAAAAAAAFGQ/tCN4WsbL2Hg/s1600/Screen+Shot+2013-12-16+at+03.29.50.png)

  
The console window gives us a confirmation that we are running from the ** jdk1.7.0_45_dcevm.jdk **path (see first line in screenshot below)

[![](images/Screen_Shot_2013-12-16_at_03_30_21.png)](http://1.bp.blogspot.com/-NzuO_fePA9k/Uq8cD4qZxXI/AAAAAAAAFGM/6x-qXkK5nWc/s1600/Screen+Shot+2013-12-16+at+03.30.21.png)

  
And so do the**_ Installation Details_** from the newly started Eclipse instance:

[![](images/Screen_Shot_2013-12-16_at_03_31_25.png)](http://2.bp.blogspot.com/-8IbSZaQ3kAM/Uq8cELOnpQI/AAAAAAAAFGI/Dg3LuG23jV4/s1600/Screen+Shot+2013-12-16+at+03.31.25.png)

Next is was time to make some live changes, for example a) on a preferences page description (see top editor) or b) adding a new static field (see bottom editor):

[![](images/Screen_Shot_2013-12-16_at_03_47_52.png)](http://1.bp.blogspot.com/-Ye0F5d6qkW4/Uq8cFekXtsI/AAAAAAAAFGg/S36dDDDYW5c/s1600/Screen+Shot+2013-12-16+at+03.47.52.png)

  
And although it didn't work when I had it running under **Run **(which was expected), when I restarted eclipse under _**Debug **, _it hang as soon as I:

1) executed a script that loaded one of the classes I wanted to changed (i.e the target class was loaded into the JVM)  
2) made a change in the host eclipse and saved it (which triggered the compilation of that file and the creation of a new version of the target class)  
3) went back to the 'under debug' version of eclipse (which by now hanged with a OSX [Spinning_pinwheel](http://en.wikipedia.org/wiki/Spinning_pinwheel) )

[![](images/Screen_Shot_2013-12-16_at_03_46_23.png)](http://2.bp.blogspot.com/-tln7aDAXqyQ/Uq8cFKYES8I/AAAAAAAAFGk/9Sid8wa9GmY/s1600/Screen+Shot+2013-12-16+at+03.46.23.png)

  
Which was a bummer since I was really looking forward to using the DCE VM technology.

Note that I also tried running the host Eclipse under the DCE VM, which gave me the same result (that said, on the positive side, I had both Eclipses running under the patched JDK which is quite cool)

The solution was to try [JRebel](http://zeroturnaround.com/software/jrebel/) which worked (see my next post)
