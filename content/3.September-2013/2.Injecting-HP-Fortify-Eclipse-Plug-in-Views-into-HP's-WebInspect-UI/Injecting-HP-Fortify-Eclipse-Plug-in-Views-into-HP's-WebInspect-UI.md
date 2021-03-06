## Injecting HP Fortify Eclipse Plug-in Views into HP's WebInspect UI

Using the [O2's Win32 Window Hijacking](http://blog.diniscruz.com/search/label/WinAPI) capabilities (see also [Opening up a native Chrome Browser window inside Eclipse (raw version)](http://blog.diniscruz.com/2013/09/opening-up-native-chrome-browser-window.html)) , here is a PoC on how to inject a couple Eclipse Views from the HP Fortify Eclipse plug-in (which is Java app running under an JVM) into the HP WebInspect UI (which is .NET app running under an CLR).

The power of this PoC is to show that we can have the best of both worlds and show security consultants and developers the best possible environment/UI for them to analyze, review and fix security vulnerabilities.

We start with an instance of Eclipse Juno with the Fortify Plug-in installed, where I opened the **Fortify Audit** perspective, in order to have access to the multiple Fortify specific views:

![](images/image_thumb.png)

Next I opened an instance of WebInspect 10.0:

![](images/image_thumb1.png)

Since we need to add a couple panels into WebInspect (which is a .NET process), the first step is to inject an [O2 REPL UI](http://blog.diniscruz.com/p/c-repl-script-environment.html) into the WebInspect process.

Note 1: if we were doing a pure Win32 Handle Hijacking this would not be needed, but in this case I want to control where the Fortify Views will be placed.

Note 2: since Web Inspect is running with elevated privileges (i.e. full admin), we will also need to run the [O2 Platform](http://blog.diniscruz.com/p/owasp-o2-platform.html) with the same privileges (or the dll injection will not work).

The script/tool that I'm going to use is the **_Util - Inject O2 into other processes.h2_**, which can be executed from here:

![](images/image_thumb11.png)

...or here:

![](images/image_thumb10.png)

On the **_Util - Inject O2 into other processes.h2_** UI, find the WebInspect process on the left-hand-side process list (a screenshot of the process should be visible if we have enough privileges to inject into this process) and click on the '**Inject O2 REPL into Process'** button:  

![](images/image_thumb12.png)

An C# REPL Editor should appear (a good clue that the injection worked ok is the fact that the top-left icon of the the REPL Form matches the icon of WebInspect):

![](images/image_thumb13.png)

Another way to confirm that this C# REPL script is indeed inside the WebInspect process, is to execute:

{lang="csharp"}
    return Processes.getCurrentProcess();

... which will return the C# object of the current process (note the ProcessName value below):

![](images/image_thumb14.png)

Since WebInspect is using .NET WinForms as its main windows host (there are a number of WPF controls in there, but the main window is an instance of **_System.Windows.Forms.Form_**), we can use this command to get the list of open forms:

{lang="csharp"}
    var openForms = Application.OpenForms;  
    return openForms;

Which in this case returns 3 Form Controls:  

  * the main WebInspect UI
  * an hidden WebInspect update window
  * the O2 platform C# REPL (currently executing the script)

![](images/image_thumb15.png)

Next, using this script:  

    var form = (Form)Application.OpenForms[1];  
    return form;

... we find the Form we want:

![](images/image_thumb16.png)

... which is of type **_SPI.WebInspect.MainForm_**:  

![](images/image_thumb17.png)

...from the **_WebInspect.exe_** assembly:  

![](images/image_thumb18.png)

... which means that we can get a strongly type reference to that control:  

![](images/image_thumb19.png)

... after adding a reference to the **_SPI.UI.dll_** (as requested by the error shown above):

![](images/image_thumb20.png)

What is really powerful about this script:  

{lang="csharp"}
    var form = (MainForm)Application.OpenForms[1];  
    return form;

    //using SPI.WebInspect  
    //O2Ref:WebInspect.exe  
    //O2Ref:SPI.UI.dll  

... is that the .NET object shown in the output window, is the real WebInspect main Form object (see below how I changed the title of the main WebInspect window (from the PropertyGrid shown in the C# REPL output panel)):  

![](images/image_thumb22.png)

Next (because we can) we are going to inject this script environment right into WebInspect UI, using the script:  

{lang="csharp"}
    var form = (MainForm)Application.OpenForms[1];  
    form.insert_Right()  
        .add_Script_Me(form);  
    return form;

    //using SPI.WebInspect  
    //O2Ref:WebInspect.exe  
    //O2Ref:SPI.UI.dll  

This will create a new Panel to the right of the current main UI and add a C# REPL Script UI to it (with the WebInspect UI **_form_** variable passed as a parameter):  

![](images/image_thumb23.png)

Using the C# REPL that is now inside the main WebInspect UI, let's create another panel (now to the left) and get its handle (which in this case it is going to be **_592370_**)  

{lang="csharp"}
    var fortifyPanel = mainForm.insert_Left();  
    return fortifyPanel.handle().str();

    //O2Ref:WebInspect.exe  
    //O2Ref:SPI.UI.dll  

![](images/image_thumb25.png)

The **_592370_** handle is what we need to in order to be able to inject Windows into that left hand side panel (basically we will set the parent of the 'Window to Hijack' to **592370**).  

For example if we wanted to add a real cmd.exe command prompt to it we could execute:

{lang="csharp"}
    var leftPanelHandle = 592370.intPtr();

    var cmdExe_WindowHandle = "cmd.exe".startProcess()  
                                       .waitFor_MainWindowHandle()  
                                       .MainWindowHandle;

    cmdExe_WindowHandle.setParent(leftPanelHandle);

    return cmdExe_WindowHandle.str();  

... which will look like this

![](images/image_thumb27.png)

.. note that this is the full cmd.exe (which can be resized, moved and used to execute commands):  

![](images/image_thumb28.png)

... or even maximized:  

![](images/image_thumb29.png)

... we can even add other processes to it, like Notepad, using the script  

{lang="csharp"}
    var leftPanelHandle = 592370.intPtr();

    var cmdExe_WindowHandle = "notepad.exe".startProcess()  
                                           .waitFor_MainWindowHandle()  
                                           .MainWindowHandle;

    cmdExe_WindowHandle.setParent(leftPanelHandle);  
    return cmdExe_WindowHandle.str();  

... which will look like this:  

![](images/image_thumb42.png)

The examples above used the main process window (whose parent was originally the handle 0 (i.e. the Desktop)).

But we can do the same thing for any child window.  

For example we could inject the actual Notepad Text Editor (vs the whole Notepad UI).

![](images/image_thumb50.png)

The following script:

{lang="csharp"}
    var leftPanelHandle = 592370.intPtr();

    var notepadProcess = "notepad.exe".startProcess();  
    var notepad_WindowHandle = notepadProcess.waitFor_MainWindowHandle()  
                                             .MainWindowHandle;

    var notepadInnerWindow = notepad_WindowHandle.child_Windows().first();

    10000.wait();

    var originalParent = notepadInnerWindow.get_Parent();

    notepadInnerWindow.setParent(leftPanelHandle);  
    notepadInnerWindow.window_Redraw();

    10000.wait();

    notepadInnerWindow.setParent(originalParent);  
    return notepadInnerWindow.str();  


Will:

  1. Open Notepad
  2. Get Notepad's main window handle
  3. Get the first child window from that handle
  4. Save the parent of the first child window
  5. Wait 10 secs (to give us time to type something on the Notepad window, when running OUTSIDE the WebInspect UI
  6. Set the parent of the Notepad child window (the TextEditor) to be the Webinspect Panel
  7. Wait 10 sec (to give us time to type something on the Notepad window, when running INSIDE the the WebInspect UI)
  8. Reset the original Notepad Child window parent

Here is what it look like before step #8 executes:

![](images/image_thumb63.png)

OK, so now that we have the ability to inject any window into WebInspect, let's add something interesting like a view from Fortify's Eclipse Plug-in (which is a Java app).

To do that we need to find the handle of the window we want to inject.

There are numerous ways to do this, one of them is to use the **_Util - Windows Handles - View Handle Screenshot.h2_** script:

![](images/image_thumb65.png)

... which can be easily used to:  

![](images/image_thumb73.png)

... find the handle we want (note the red box highlighting the selected window (also shown as a screenshot inside the **_Util - Windows Handles - View Handle Screenshot.h2_** script UI))  

![](images/image_thumb77.png)

Once we know the handle of the window we want to inject (in this case 794042), we can automate the injection using this script:  

{lang="csharp"}
    var leftPanelHandle = 592370.intPtr();  
    var fortifyPanel    = 794042.intPtr();  
    //return fortifyPanel.get_Parent().str(); //400746 (backup in case we want to restore it)

    fortifyPanel.setParent(leftPanelHandle);

    return "done";

    //using O2.XRules.Database.APIs  
    //O2File:O2File:API_WinAPI.cs  

... which will create this:  

![](images/image_thumb78.png)

Note 1: the Fortify Eclipse Plugin panel (top-left) is now in WebInspect and not in Eclipse

In the screenshot above the Fortify Plug-in View was not correctly resized to its new parent. This can be corrected using this script:

{lang="csharp"}
    var leftPanelHandle = 592370.intPtr();  
    var fortifyPanel    = 794042.intPtr();

    var rect = fortifyPanel.get_Parent().window_Rectangle();

    fortifyPanel.window_Move(0,0,rect.Width,rect.Height);  


... which will set the size of the injected window to be the size of its parent (another option would had been to call the **.window_Maximize()** extension method):  

![](images/image_thumb80.png)

**Returning back the Fortify Eclipse Plugin View**

Here are a couple interesting places to put the view back:

**Example #1**) The Desktop** (using the parent handle 0)

![](images/image_thumb81.png)

Note that that window will not be movable or resizable (i.e. it is stuck in that location))

**Example #2)** Cmd.exe (using the cmd.exe MainWindowHandle as the parent)

![](images/image_thumb82.png)

Note that in cases like this, the host process can be resized but the injected window will remain in the same relative place (to its parent window)

So we can create GUIs like this, where the Fortify Plugin View is nicely positioned to the top right of a cmd.exe process:

![](images/image_thumb85.png)

**Example #3)** Notepad: (same technique as shown above)

![](images/image_thumb86.png)

**Example #4)** Eclipse** (returning the view to its original parent)

![](images/image_thumb87.png)
