Sure, there are many ways to get started coding on msysGit.
While participating a 24h-hackathon, we've discovered a smart way
to code on msysGit under Windows, by using Eclipse.


#### Goals
* using an IDE - not only a text editor
* code syntax highlighting (sophisticated and able to recognize scopes)
* code navigation (clicking with mouse of using keyboard shortcuts)
* re-factoring (at least rename local variables, etc.)
* full and robust debugging support using actual C source code files
* preferred: smart search, not only RegEx ;-)
* nice to have: able to create build within the IDE

As it turns out, with a little knowledge about Eclipse, we've found everything solved by using Eclipse and a separate MinGW installation. The setup is pretty fast and can be done in less than one hour. If you know other Languages and IDEs, you may miss some features, but this setup solved our needs. Some aspects/goals are not yet solved (wasn't our focus) - so consider this as a starting point ;-)


#### Install required tools

1. Of course, first you need to setup msysGit
   * I've used the net installer
   * See [InstallMSysGit](https://github.com/msysgit/msysgit/wiki/InstallMSysGit)
1. Download Eclipse C/C++ (current version Juno, 4.2 SR2)
   * unzip it somewhere (c:\program files\eclipse)
   * install Java JRE (current version 1.7) - a JRE is sufficient, but installing a JDK is highly recommended
1. Download MinGW
   * I've used net installer mingw-get-inst-20120426.exe 
   * install it; for example C:\MinGW (recommended)
   * This is optional, but I recommend it because of newer gdb (debugger) version


#### Setup Eclipse Workspace

* Run eclipse and use a separate workspace folder, which is _NOT_ the msysgit installation folder
* create a new project
   * use the wizard to create a new C Proejct (simple C Project only)
   * name the project 'msysGit'
   * use all the wizard default settings and finish this step
* within the project create a linked folder to msysGit
   * folder-name: ```src-git```
   * click ```advanced```
   * click ```linked folder```
   * specify the msysGit installation path and the ```git``` folder within
   * [[https://raw.github.com/hypoport/msysgit/master/doc/howto/code_msysgit_in_eclipse/create_linked_folder_to_msysgit.png]]

At this point, you're able to navigate and edit the sources.


#### Fine-tune Project Preferences

* Disable auto build
   * Because we've didn't configured any build tools, you should disable Project -> Auto build
   * For our setup, we've only used command line ```make``` tool for building git.
* Enable PE Windows binary parser in debug configurations
   * Open: Project Preferences -> C/C++ Build -> Settings -> Binary Parser
   * Enable: PE Windows Parser
   * [[https://raw.github.com/hypoport/msysgit/master/doc/howto/code_msysgit_in_eclipse/project_prefs_binary_parser.png]]
   * **Side note**: If this option isn't enabled, you will encounter an error message when starting the debugger. Error message: "Program is not a recognized executable"

#### Build msysGit

* For our experiments, we've used this command ```make clean  ; make CFLAGS=-g3 LDFLAGS=-g3```

#### Debug Launch Configuration
For this example, we want to debug the ```git-add.exe```.

Open the debug configuration dialog via the run menu and create a new C/C++ Application configuration:
* Main
   * Name: git-add.exe
   * C/C++ Application: C:\msysgit\git\git-add.exe
   * [[https://raw.github.com/hypoport/msysgit/master/doc/howto/code_msysgit_in_eclipse/debug_configuration.png]]
* Environment
   * Add: HOME\_DRIVE C:
   * Add: HOME\_PATH \Users\username   (your home path)
   * Add: PATH c:\MinGW\bin
   * Set: Recplace native environment with specific environment
   * **Side note**: We're not 100% sure, why the environment has to be replaced, but it worked very well this way :-)
   * **Side note**: These settings are specific to Windows platform. They may have to be adjusted on different platforms.
   * [[https://raw.github.com/hypoport/msysgit/master/doc/howto/code_msysgit_in_eclipse/debug_configuration_environment.png]]
* Debugger
   * We're using the separate MinGW debugger, because it's more up to date.
   * GDB Debugger: C:\MinGW\bin\gdb.exe
   * [[https://raw.github.com/hypoport/msysgit/master/doc/howto/code_msysgit_in_eclipse/debug_configuration_gdb.png]]
