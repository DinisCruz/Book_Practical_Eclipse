## Installing Eclipse Plugin Builder, accessing Eclipse objects and adding a new Menu Item that opens Owasp.org website 

This post shows how to use the Eclipse Plugin Update site described in [TeamMentor Plugin and Builder v1.5.6 (Source Code and Eclipse Update site)](http://blog.diniscruz.com/2013/11/teammentor-plugin-and-builder-v156.html) to install and use the Eclipse Builder Kit that we open sourced last week.

The objective is to do these actions, without needing to start Eclipse to see them:

  * Dynamically access eclipse objects like: Shell, Workbench, Worksapce, ActiveWorkbenchPage, Display, etc...
  * Open the [http://www.owasp.org](http://www.owasp.org/) website in a browser (and put it inside an Action object)
  * Add new Menu called 'OWASP'
  * Add a menu Item to the 'OWASP' menu called 'Open OWASP website' that calls the Action object that opens wht OWASP website.
  
**Step 1:_ _Install the TeamMentor Plugin version 1.5.6 in Kepler**  
**  
**In a default install of Kepler (this should also work in versions 3.7 (Indigo) and 4.2 (Juno))

[![image](images/image_thumb_25255B1_25255D1.png)](http://lh5.ggpht.com/-GV6TzaVwOUc/Upy5WW3neYI/AAAAAAAARAQ/dVCjd18c7K8/s1600-h/image%25255B3%25255D.png)

...open the **_Install New Software... _**menu option:

[![image](images/image_thumb_25255B6_25255D1.png)](http://lh5.ggpht.com/-iGyKjXP-HMY/Upy5X6W94jI/AAAAAAAARAc/r7F4aYlwPeU/s1600-h/image%25255B7%25255D.png)

...enter the value [http://eclipse-plugin-builder.azurewebsites.net](http://eclipse-plugin-builder.azurewebsites.net/) the **_Work with: _**Textbox

[![image](images/image_thumb_25255B7_25255D1.png)](http://lh6.ggpht.com/-4soqXMp1nZ4/Upy5Y_CuSNI/AAAAAAAARAs/4_Zm0fwFzZI/s1600-h/image%25255B10%25255D.png)

...select the **_TeamMentor Eclipse PlugIn -- For Fortify _**option and click Next

[![image](images/image_thumb_25255B8_25255D1.png)](http://lh3.ggpht.com/-4hRuS3mJmZ8/Upy5ZlaUWiI/AAAAAAAARA8/25V5ydVbE94/s1600-h/image%25255B13%25255D.png)

... click **_Next_**:

[![image](images/image_thumb_25255B9_25255D1.png)](http://lh3.ggpht.com/-G0AnNkH3WTc/Upy5a2wPn7I/AAAAAAAARBQ/798fNYaiCUw/s1600-h/image%25255B16%25255D.png)

... accept the terms and click **_Finish_**:

[![image](images/image_thumb_25255B10_25255D1.png)](http://lh4.ggpht.com/-vwieBpRr5YQ/Upy5ceru22I/AAAAAAAARBg/TRHDdGJEK38/s1600-h/image%25255B19%25255D.png)

... click OK on the unsigned warning (this will be addressed on the final build)

[![image](images/image_thumb_25255B11_25255D1.png)](http://lh3.ggpht.com/-e9cVhPTPQew/Upy5dtvssWI/AAAAAAAARBs/NxiQ_dyEopE/s1600-h/image%25255B22%25255D.png)

... and finally click **_Yes_** to reboot:

[![image](images/image_thumb_25255B12_25255D1.png)](http://lh6.ggpht.com/-pPt2eTMwzPk/Upy5ejvPJNI/AAAAAAAARCA/xaiqQVZTy7Y/s1600-h/image%25255B25%25255D.png)

**  
****Step 2: Enable script support and write a 'Hello World' script**  
**  
**Once Eclipse starts, you should see a **_TeamMentor_** menu, where you need to click on the **_Open Properties Page _**menu item

[![image](images/image_thumb_25255B19_25255D1.png)](http://lh3.ggpht.com/-xpjvnkA_Kwo/Upy5fdAFB1I/AAAAAAAARCM/pT_2UYk651U/s1600-h/image%25255B29%25255D.png)

... select the **_Show Advanced Mode Features_** checkbox:

[![image](images/image_thumb_25255B20_25255D1.png)](http://lh6.ggpht.com/-fYTWhFgdDss/Upy5glTPLYI/AAAAAAAARCg/mJzalFcleKw/s1600-h/image%25255B32%25255D.png)

... click **_OK_**  
**_  
_**[![image](images/image_thumb_25255B21_25255D.png)](http://lh6.ggpht.com/-xzhO4spae3M/Upy5h-dy0HI/AAAAAAAARCs/30m2lH8eYiQ/s1600-h/image%25255B35%25255D.png)

... and open the **_Util -- Write Script (TeamMentor DSL) _**menu item from the (new) **_Advanced and Debug Features_** menu

[![image](images/image_thumb_25255B26_25255D.png)](http://lh4.ggpht.com/-_9WGtqSOm-U/Upy5iwcMUHI/AAAAAAAARDA/IEpPzBt3Nfo/s1600-h/image%25255B39%25255D.png)

NOTE: if you are running this on Indigo, you will need to restart Eclipse since menu visibility is not loaded dynamically (as it is in Kepler). I'm sure there is a way to force its refresh, so if you know about it, let me know.

The scripting UI should look like this:

[![image](images/image_thumb_25255B27_25255D.png)](http://lh3.ggpht.com/-pzYjPPyZfmw/Upy5kSb1YpI/AAAAAAAARDQ/4SLef_pJY5E/s1600-h/image%25255B42%25255D.png)

... where if you click on **_Execute_** you should see of one of TeamMentor's article showing up in a browser window

[![image](images/image_thumb_25255B28_25255D1.png)](http://lh3.ggpht.com/-JgS3XIkRYxQ/Upy5ln-YKWI/AAAAAAAARDg/22ur4xx3MvI/s1600-h/image%25255B45%25255D.png)

... and an eclipse object string representation (in this case **_tm.eclipse.api.EclipseAPI@1ffbe29_**) in the script UI's **_Execution result_** panel

[![image](images/image_thumb_25255B29_25255D.png)](http://lh5.ggpht.com/-OoxCmrAQwJs/Upy5m4YpAbI/AAAAAAAARDw/OpoowczXcyU/s1600-h/image%25255B48%25255D.png)

To create the first **_Hello World_** example, replace the text inside the  **_Groovy Code_** panel with:

[![image](images/image_thumb_25255B31_25255D.png)](http://lh4.ggpht.com/-9gH-oDVbrdU/Upy5onkF7mI/AAAAAAAARD8/zMjFnVarSiI/s1600-h/image%25255B54%25255D.png)

... and click on **_Execute _**to see the **_Hello World_** in the **_ Execution result_ **panel

[![image](images/image_thumb_25255B32_25255D1.png)](http://lh6.ggpht.com/-nnxbx8Cm6ho/Upy5pshDIUI/AAAAAAAAREQ/ssXpytFridA/s1600-h/image%25255B57%25255D.png)

Note that the_ **Execution result** _will show the last object of the Groovy script execution, so you can just do this:

[![image](images/image_thumb_25255B33_25255D1.png)](http://lh3.ggpht.com/-0fDBkiMDxLo/Upy5qjw4GfI/AAAAAAAAREg/UwwPJGafJHk/s1600-h/image%25255B60%25255D.png)

**  
****Step 3: Access Internal Eclipse objects to view/change properties values and invoke methods**  
**  
**What is really powerful about this scripting environment, is the fact that it is running on the Eclipse JVM, which means that it has access to all Eclipse objects in real time.

In practice, this means that we can access Eclipse objects and manipulate them right inside the Eclipse instance we are running the scripts! No more waiting 30s to see the effect of a code change or simple code test :)

To make life/coding easier, most of the common objects one needs when programming eclipse are exposed via the [EclipseApi class](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/blob/develop/TeamMentor.Eclipse.PlugIn.Fortify/src/tm/eclipse/api/EclipseAPI.java), which is available via the **_eclipse_** object (or the **_eclipseAPI_** object) already mapped to the current Groovy script being executed:

[![image](images/image_thumb_25255B49_25255D.png)](http://lh6.ggpht.com/-zlYJj6jQrcY/Upy5r_7apmI/AAAAAAAAREs/LwdzY518cFw/s1600-h/image%25255B97%25255D.png)

Groovy has a nice Object Viewer helper UI in the _**groovy.inspect.swingui.ObjectBrowser **_class, which is exposed as the **_inspect({any object})_** method that can be used (see below) to view all **_Public Fields and Properties _**of the eclipse object_:** **_  
_  
_[![image](images/image_thumb_25255B55_25255D1.png)](http://lh4.ggpht.com/-pnaRuK64ssM/Upy5sw3AWNI/AAAAAAAARFA/RsLZnzPHU6I/s1600-h/image%25255B104%25255D.png)

and all **_(Meta) Methods:_**  
**_  
_**[![image](images/image_thumb_25255B60_25255D1.png)](http://lh3.ggpht.com/-3rhMYos2QCE/Upy5tzqLLrI/AAAAAAAARFM/udET4ALr1rY/s1600-h/image%25255B105%25255D.png) 

Here is a quick view of the main helper fields mapped to Eclipse objects:

**eclipse.shell**  
**  
**[![image](images/image_thumb_25255B61_25255D1.png)](http://lh3.ggpht.com/-sM8FysQn_Ec/Upy5vN7iHNI/AAAAAAAARFc/ehOs2ujnu6Y/s1600-h/image%25255B108%25255D.png)

.... which is an instance of _**org.eclipse.swt.widgets.Shell**_:

[![image](images/image_thumb_25255B64_25255D.png)](http://lh6.ggpht.com/-9xa9L0ZDZrY/Upy5wFIJYAI/AAAAAAAARFs/WGuEq9Z2A7s/s1600-h/image%25255B117%25255D.png)   
**_  
_****_eclipse.workbench_** (instance of **_org.eclipse.ui.internal.Workbench_**)

[![image](images/image_thumb_25255B65_25255D1.png)](http://lh4.ggpht.com/-VkmCSL_0jSk/Upy5xNpvohI/AAAAAAAARF8/GGGmbPjDKok/s1600-h/image%25255B120%25255D.png)   
**_  
_****_eclipse.workspace _**(instance of **_org.eclipse.ui.internal.resources.Workspace_**)

[![image](images/image_thumb_25255B66_25255D1.png)](http://lh5.ggpht.com/-1TA-V0MmTDs/Upy5yAoE3dI/AAAAAAAARGQ/gMNR2hY4LXE/s1600-h/image%25255B123%25255D.png)   
**_  
_****_eclipse.activeWorkbenchPage _**(instance of **_org.eclipse.ui.internal.WorkbenchPage_**)

[![image](images/image_thumb_25255B67_25255D.png)](http://lh6.ggpht.com/-vtG3zUjTACk/Upy5zfbku8I/AAAAAAAARGg/aobPqAMR5jI/s1600-h/image%25255B126%25255D.png)  
**_  
_****_eclipse.activeWorkbenchWindow _**(instance of **_org.eclipse.ui.internal.WorkbenchWindow_**)

[![image](images/image_thumb_25255B69_25255D.png)](http://lh3.ggpht.com/-Brnpo2hPXOs/Upy50Ex6OlI/AAAAAAAARGs/4t9AHPwiDiM/s1600-h/image%25255B132%25255D.png)   
**_  
_****_eclipse.display _**(instance of **_org.eclipse.swt.widgets.Display_**)

[![image](images/image_thumb_25255B68_25255D.png)](http://lh3.ggpht.com/-WB904r85Skk/Upy51GV6FeI/AAAAAAAARHA/v1GFBTMgQkw/s1600-h/image%25255B129%25255D.png)

The reason why is very powerful to have access to these objects is that have real-time read/write access to its properties/fields

For example use **_inspect(eclipse.shell)_** to see the current Eclipse's Shell object properties/fields:

[![image](images/image_thumb_25255B71_25255D.png)](http://lh6.ggpht.com/-TAUxoTr434E/Upy52ILx-NI/AAAAAAAARHM/sujTxWqK-ss/s1600-h/image%25255B138%25255D.png)

note: since we are using Groovy we can also use: **_eclipse.shell.dump()_**  
**_  
_**[![image](images/image_thumb_25255B70_25255D.png)](http://lh3.ggpht.com/-gkq8idvl-l8/Upy53f_VkhI/AAAAAAAARHg/oxpd45QkxtE/s1600-h/image%25255B135%25255D.png)

If you look at the list of the properties/fields in the **_eclipse.shell_** object, notice that there is one called **_text_**,which is the value of the current Shell window title (in the case below 'Java -- Eclipse')

[![image](images/image_thumb_25255B72_25255D.png)](http://lh5.ggpht.com/-GssuL5Z0USM/Upy54pEqkqI/AAAAAAAARHo/2DEk4NxgVrg/s1600-h/image%25255B141%25255D.png)

Not only we have access to this value, we can be dynamically change it:

[![image](images/image_thumb_25255B73_25255D.png)](http://lh4.ggpht.com/-cSlx2I1eRRs/Upy55Z1mL7I/AAAAAAAARH8/x6LbVXCnSvk/s1600-h/image%25255B144%25255D.png)

We can also easily open views like this:

[![image](images/image_thumb_25255B74_25255D.png)](http://lh6.ggpht.com/--h2wXPRE-80/Upy56Zbo4DI/AAAAAAAARIM/cfLAGAd-Ego/s1600-h/image%25255B147%25255D.png)

.. or get a list of open views:

[![image](images/image_thumb_25255B77_25255D.png)](http://lh6.ggpht.com/-mrW9Wjl6PTA/Upy57poH9nI/AAAAAAAARIc/rbhxW61KdN8/s1600-h/image%25255B156%25255D.png)

**Step 4: Add a new Menu Item that opens OWASP.org website**  
**  
**Now, lets say that we want to so something more interesting like adding a new Menu Item that opened the [http://www.owasp.org](http://www.owasp.org/) website.

We can start with this code snippet that will open the Eclipse internal browser:  

    
    def browserId = "Test Browser";  
    def website= "http://www.owasp.org";  
    def browser = eclipse.workbench.getBrowserSupport().createBrowser(browserId);  
    browser.openURL(new URL(website));

  


  
... which when executed will look like this:

[![image](images/image_thumb_25255B78_25255D.png)](http://lh5.ggpht.com/-BzqYY-BWOuk/Upy58hAWhWI/AAAAAAAARIw/sFpgSkSQOtU/s1600-h/image%25255B159%25255D.png)

Next lets move the code that opens a browser into an Action object:
    
    import org.eclipse.jface.action.Action;  
    def final _eclipse = eclipse;  
    Action action = new Action()  {  
                                     @Override  
                                     public void run() {                              
                                                          def browserId = "Test Browser";  
                                                          def website= "https://www.google.com"; //"http://www.owasp.org";    
                                                          def browser = _eclipse.workbench.getBrowserSupport().createBrowser(browserId);  
                                                          browser.openURL(new URL(website));  
                                                       }  
                                 }

return action.run();  
  
Here is the code that will create a new Menu (not visible until it has an action)
    
    def menuName = "New Menu";  
    def topMenuManager      = eclipse.activeWorkbenchWindow.getMenuManager()  
    MenuManager newMenu = new MenuManager(menuName);  
    topMenuManager.prependToGroup(IWorkbenchActionConstants.MB_ADDITIONS, newMenu);

  


  
Putting the two together:
    
    import org.eclipse.jface.action.*;  
    import org.eclipse.ui.IWorkbenchActionConstants;

def final _eclipse = eclipse;

def menuName = "New Menu";  
def actionName = "open owasp.org";  
def topMenuManager = eclipse.activeWorkbenchWindow.getMenuManager()  
MenuManager newMenu = new MenuManager(menuName);  
topMenuManager.prependToGroup(IWorkbenchActionConstants.MB_ADDITIONS, newMenu);

Action action = new Action(actionName) {  
@Override   
public void run() {   
def browserId = "Test Browser";  
def website= "http://www.owasp.org";  
def browser = _eclipse.workbench.getBrowserSupport().createBrowser(browserId);  
browser.openURL(new URL(website));  
}  
}

  
newMenu.add(action)

topMenuManager.update(true);

return topMenuManager;  
  
We get a new menu:

[![image](images/image_thumb_25255B88_25255D.png)](http://lh5.ggpht.com/-1K1XXRFndio/UpzBG_99HKI/AAAAAAAARLY/jSuxeYGlShI/s1600-h/image%25255B170%25255D.png)

...which when selected will open an browser with [https://www.owasp.org](https://www.owasp.org/)

[![image](images/image_thumb_25255B89_25255D.png)](http://lh3.ggpht.com/-45BO_9zdHsI/UpzBHks8dSI/AAAAAAAARLo/NhEQ7CEBaaQ/s1600-h/image%25255B173%25255D.png)

  
What is really interesting in the code sample above, is how close we are to programming in pure java in normal Eclipse plugin development mode (great when learning how the API works and following the existing code sample).

But since my view in API development is to make it as easy as possible to perform the desired action, I added an helper method to the EClipseAPI to create a menu item that opens a browser window

Using the helper API, the entire code above can be replaced with:  

    
    def testMenu = eclipse.menus.add_Menu("Test Menu")  
    eclipse.menus.add_MenuItem_OpenWebPage(testMenu, "Open OWASP website", [https://www.owasp.org](https://www.owasp.org/))

  


  
...which when executed will add the **_Test Menu_** to the top menu with a **_Open OWASP website_** menu item

[![image](images/image_thumb_25255B106_25255D.png)](http://lh5.ggpht.com/-LeDX3zZZ5Ro/UpzBI-yJYcI/AAAAAAAARL0/xHrTjVUGrL4/s1600-h/image%25255B178%25255D.png)

Note1 : In C# I could had made that API even simpler since I could had used Extension methods to add the **_add_Menu_Item_** method to the **_MenuManager_** class

Note 2: There are a couple more helper methods which you can see at: [https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/blob/develop/TeamMentor.Eclipse.PlugIn.Fortify/src/tm/eclipse/api/Menus.java](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/blob/develop/TeamMentor.Eclipse.PlugIn.Fortify/src/tm/eclipse/api/Menus.java)  


  


**Appendix: Auto updates**

Once you can have the Plug-in installed, you can get updates via the 'Check for Updates' menu option (note that moment fixes are pushed as minor updates, so you might not get the latest version after the first install):

[![image](images/image_thumb_25255B42_25255D1.png)](http://lh3.ggpht.com/-6UqjGO-HVl0/Upy59-EzYII/AAAAAAAARJA/556McPiREmo/s1600-h/image%25255B76%25255D.png)

If there is an update, you will get a window that looks like this:

[![image](images/image_thumb_25255B43_25255D1.png)](http://lh4.ggpht.com/-MlbcPPVtf5s/Upy5_A-X7xI/AAAAAAAARJQ/QnhRgZAFn54/s1600-h/image%25255B79%25255D.png)

... where you can review the updates and click ''Next'

[![image](images/image_thumb_25255B44_25255D1.png)](http://lh5.ggpht.com/-9TyNz-APzT0/Upy6ATdnTkI/AAAAAAAARJc/-WSDfryRhBk/s1600-h/image%25255B82%25255D.png)

... access the license and click Finish

[![image](images/image_thumb_25255B45_25255D.png)](http://lh3.ggpht.com/-Zq8I6P0QJMU/Upy6BWStYPI/AAAAAAAARJw/Cgp4-6u7-qE/s1600-h/image%25255B85%25255D.png)

... click OK (if you are not in an hostile network that is able to dynamically backdoor Eclipse plugins on the fly):

[![image](images/image_thumb_25255B46_25255D1.png)](http://lh5.ggpht.com/-keK4rEDqLmE/Upy6CtrOu0I/AAAAAAAARJ8/DpLm7A_3slg/s1600-h/image%25255B88%25255D.png)

... and finally click **YES** to reboot:

[![image](images/image_thumb_25255B47_25255D.png)](http://lh5.ggpht.com/-_Quk-z23X0Y/Upy6D4QFjHI/AAAAAAAARKM/yger0ir8OO0/s1600-h/image%25255B91%25255D.png)

  
Note: if you want the checks to happen automatically, you can set it here:

[![image](images/image_thumb_25255B48_25255D1.png)](http://lh6.ggpht.com/-t2dxcujm94E/Upy6E8HSOlI/AAAAAAAARKg/LkmXy3pGyzk/s1600-h/image%25255B94%25255D.png)
