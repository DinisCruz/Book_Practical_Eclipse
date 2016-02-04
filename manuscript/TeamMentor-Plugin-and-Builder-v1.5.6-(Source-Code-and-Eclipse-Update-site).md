## TeamMentor Plugin and Builder v1.5.6 (Source Code and Eclipse Update site)

**TLDR:** open eclipse and install the plugin from: [http://eclipse-plugin-builder.azurewebsites.net](http://eclipse-plugin-builder.azurewebsites.net/)

I just updated the [TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin) repo with the latest version of this plugin (take a look at the [develop](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/tree/develop) branch which is in sync with the [develop branch in my dev fork](https://github.com/DinisCruz-Dev/TeamMentor_Eclipse_Plugin/tree/develop)).

This code is now Open Source (see [SI Open Sources the Eclipse Plugin-development toolkit that I developed for TeamMentor](http://blog.diniscruz.com/2013/11/si-open-sources-eclipse-plugin.html)) so fell free to take a look, fork it and figure out how to use it.  
  
Note that we are in active development of this plugin, with still a number of [bugs/issues to address](https://github.com/TeamMentor/Master/issues?labels=Area%3A+Plugin-Eclipse+Fortify&state=open) before the first official release.

The final version of this plugin will not have the Fortify Groovy script/extension, since that will be changed into a separate project and install (at the moment if you run the current version of the plug-in in an instance of Eclipse with the Fortify plug-in installed, you will see TeamMentor guidance showing up every-time you click on a finding in the Fortify View).

The deployment files (ie eclipse installs) are all stored in the [TeamMentor_Eclipse_Plugin_Deploy](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin_Deploy) repository which you can clone and use as an eclipse plugin installation folder.

But the easiest way to start using it is to use the [http://eclipse-plugin-builder.azurewebsites.net](http://eclipse-plugin-builder.azurewebsites.net/) update site (which contains a push of [TeamMentor_Eclipse_Plugin_Deploy](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin_Deploy)).

Over the next couple days, I'm due to write a number of technical blog posts and documentation about this plugin, so watch this space.

Finally, if you have specific areas of the 'Eclipse Plugin Builder' architecture that you want me to focus on, please let me know and I will try to cover it. 
