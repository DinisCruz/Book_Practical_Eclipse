## Using AngularJS in Eclipse, Part 1) The Basics

This  covers the _**The Basics**_ example from [AngularJS](http://angularjs.org/http://angularjs.org/)'s home page:  

I'm doing this on an OSX laptop and the first step was to download and unzip ([eclipse-standard-kepler-SR1-macosx-cocoa.tar.gz](http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/kepler/SR1/eclipse-standard-kepler-SR1-macosx-cocoa.tar.gz) (32bit version of Eclipse's Kerpler) into the **_~/_Dev/_AngularJS_** folder.

I fired up eclipse, chose the _~/_Dev/_AngularJS/workspace_ as the workspace root and installed the [Eclipse Grovy REPL Scripting Environment 1.6.0](https://marketplace.eclipse.org/content/eclipse-grovy-repl-scripting-environment) ([update site](http://eclipse-plugin-builder.azurewebsites.net/)) and [Angular-JS Eclipse Tooling](https://github.com/angelozerr/angularjs-eclipse) ([update site](http://oss.opensagres.fr/angularjs-eclipse/1.0.0-SNAPSHOT/)) plugins.


**1) Creating an Angular JS Project**  

After restarting eclipse, I right-clicked on the **_Project Explorer_** view and chose the **_New_** -> **_Static Web Project_** menu item

![](images/Screen_Shot_2014-02-19_at_16_38_43.png)

... set **_AngularJS_Tests_** as the project name and clicked **_Finish_**

![](images/Screen_Shot_2014-02-19_at_16_39_32.png)

... switched to the **_Web Perspective_**

![](images/Screen_Shot_2014-02-19_at_16_39_57.png)

... with the **_Project Explorer_** view now looking like this:

![](images/Screen_Shot_2014-02-19_at_16_40_53.png)

With the final setup being the conversion into an **_AngularJS Project_**

![](images/Screen_Shot_2014-02-19_at_16_41_04.png)

**2) Creating the The_Basics.html file**  

To create the first test file, I right-clicked on the _Web Content_ folder, and chose the _New_ -> _Html File_ menu option:

![](images/Screen_Shot_2014-02-19_at_16_41_54.png)

... set the file name to *The_Basics.html* and click on **_Finish_**

![](images/Screen_Shot_2014-02-19_at_16_47_16.png)

**NOTE:** The reason this first file is called *The_Basics.html* is because I'm going to be using the examples from AngularJS' home page [http://angularjs.org/](http://angularjs.org/)

![](images/Screen_Shot_2014-02-19_at_16_42_29.png)

Once the *The_Basics.html* file opens up in eclipse

![](images/Screen_Shot_2014-02-19_at_16_49_31.png)

... I change its contents to the code sample from [http://angularjs.org/](http://angularjs.org/)

![](images/Screen_Shot_2014-02-19_at_16_50_25.png)

Note how the AngularJS Eclipse plugin successfully detects the Angular attributes and showed relevant information about it.

Here is **_ng-app_**:

![](images/Screen_Shot_2014-02-19_at_16_50_51.png)

Here is **_ng-model_**:

![](images/Screen_Shot_2014-02-19_at_16_51_08.png)

**3) Fixing the undefined Attribute name issue**  

Since I used Eclipse's **Static Web Project**, when I saved the *The_Basics.html* file, the following error  occurred (if the Eclipse's Html validation settings are the default ones):

![](images/Screen_Shot_2014-02-19_at_16_51_22.png)

... which basically means that Eclipse is not recognising the AngularJS Html attributes:

![](images/Screen_Shot_2014-02-19_at_16_51_27.png)


To fix this, I went to the **_AngularJS_Test_** project's Properties, opened the _HTML Syntax_ page (from the **_Validation_** section) and set to false the **Undefined attribute name **setting (in the **_Attributes_** options , not the **_Elements_** one)  

![](images/Screen_Shot_2014-02-19_at_17_08_36.png)

With that config change, there are no problems in this page, and hovering on top of one the AngularJS directives will show the correct tooltip:

![](images/Screen_Shot_2014-02-19_at_17_09_28.png)

**4) Viewing and previewing the *The_Basics.html* page**

Since at the moment we only have one page, we can view it directly without needing a Web Server.

To do that, I clicked on the html file and chose the **_Web Browser_** option from the **_Open With_** menu:

![](images/Screen_Shot_2014-02-19_at_17_09_41.png)

This will open the default Eclipse Browser

![](images/Screen_Shot_2014-02-19_at_17_10_10.png)

... with the AngularJS test working as expected (in this case any text typed in the **_Name_** TextBox will automatically be shown in the page:

![](images/Screen_Shot_2014-02-19_at_17_10_21.png)

We can also preview some of the changes in real time, by choosing the **_Web Page Editor:_**

![](images/Screen_Shot_2014-02-19_at_17_10_46.png)

... which will look like this (note the non-processed HTML at the top and the HTML code at the bottom):

![](images/Screen_Shot_2014-02-19_at_17_11_04.png)

Opening up the **_Preview_** tab (from the default **_Design_** tab) will allow us to test the page currently being edited (note how Angular JS is working):

![](images/Screen_Shot_2014-02-19_at_17_11_23.png)

This means that (when in the **_Design_** tab) we can edit the AngularJS HTML page and see the changes immediately:

![](images/Screen_Shot_2014-02-19_at_17_12_13.png)

NOTE: This version of the **Web Page Editor **doesn't render the CSS while in that **_Design_** mode, which means that if we add bootstrap to this project:

![](images/Screen_Shot_2014-02-19_at_17_23_58.png)

... the CSS will only be visible when in the **_Preview_** tab:  

![](images/Screen_Shot_2014-02-19_at_17_24_12.png)

**4) Creating a Git Repository for the files created**  

The best way for me to share these files is via a Git Repository, so the final step of this post is to create one on the files we have already created.

Since we are in eclipse I tried to create an Git Repo for the current project:

![](images/Screen_Shot_2014-02-19_at_17_43_58.png)

But the *Git Repository* wizard:  

![](images/Screen_Shot_2014-02-19_at_17_44_24.png)

... didn't work, because it expects the target folder to not exist:

![](images/Screen_Shot_2014-02-19_at_17_48_31.png)

This was easily solved via the command line (by executing _$ git init_ on the **_AngularJS_Tests_** folder)

![](images/Screen_Shot_2014-02-19_at_18_22_10.png)

Now that we have a git repository, I was time to open it:

![](images/Screen_Shot_2014-02-19_at_17_45_45.png)

... using the**_ Git Repositories_** view

![](images/Screen_Shot_2014-02-19_at_17_46_03.png)

... where we can use the _Add an existing local Git repository_ link:

![](images/Screen_Shot_2014-02-19_at_18_22_37.png)

... to open the repository just created:

![](images/Screen_Shot_2014-02-19_at_18_23_07.png)

In order to create a git commit, I also opened the **_Git Staging_** view:

![](images/Screen_Shot_2014-02-19_at_18_24_16.png)

This is what these two git views look like (note that there are no commits/references and the list of new files in the **Unstaged Changes** list)

![](images/Screen_Shot_2014-02-19_at_18_25_20.png)

To commit the files drag-n-drop them from the **_Unstaged Changes_** to the _Staged Changes_, and write a commit message:

![](images/Screen_Shot_2014-02-19_at_18_25_49.png)

After clicking the **_Commit_** button the **_Git Repositories_** view will give a visual representation of the location current HEAD (which is the commit just done)

![](images/Screen_Shot_2014-02-19_at_18_26_06.png)
