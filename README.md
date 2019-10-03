# devfile-tutorial
A tutorial to guide the user through the process of creating and using a custom devfile in Eclipse Che 7+

## The devfile
A file named "devfile.yaml" is used to configure a workspace in Eclipse Che. The file contains a declarative description of the workspace, including metadata, frameworks, programming languages, projects, custom commands and more. Because this is a text-based configuration -- as opposed to, say, a Linux image containing everything needed -- it makes it (somewhat) easier to understand. It also allows you to easily store the workspace definition in source control. You may have heard the phrase "infrastructure as code"; this is a good example.

projects
This is the section that defines which projects will be included in this workspace. In this particular example, it's a git repository hosted at github, and we've specified the branch "master". This means that when the workspace is started, this project is loaded and ready for coding.

An important point to remember: The Che IDE is built on the Microsoft Monaco editor and is compatible with VS Code. That means you can use online material related to VS Code to learn more about creating a devfile.

commands
This is where we can specify custom commands for the workspace. The beauty of this is that every developer will be using the same commands. You won't have the situation where, for example, one developer is using command line switches while another isn't, resulting in differing outcomes. We can assure consistency here.

You can configure as many custom commands as you wish. We'll break down the example here.

name is what you want to see appear on the workspace. You can call it whatever you want. 

actions
The work that actually gets done when the command is run. This can get complicated because of IDE-specific commands versus environment-related commands. Further, you can use runtime variables to expand any templated values.

There are three different types of actions: Actions that can run in the IDE, VS Code launch configurations, and actions that can run when VSCode is running.

Actions that can run in the IDE are things that you would do at the command line. For example, if you're using NodeJS, you might have "Update Dependencies" as an action name with "npm install" as the command.

In our example we see an action of type "vscode-launch". This is an action that is installed into our IDE when it is launched; and action that happens within the context of the IDE (versus inside a terminal window). With this "Attach to Remote" command installed, we can use it from the "DEBUG" section of the IDE. Further, you can see how this is installed by opening the file "launch.json". You can use the menu option "Debug -> Open Configurations" to do this.

Continuing through our example, we can see several actions of type "exec". These are the tasks that can be executed from within the IDE, but they happen at the command line. You can use an extensive array of templated parameters here to generalize your commands.

For example, the command named "download dependencies" will run the command "npm install" at the command line. Notice the working directory includes a template -- CHE_PROJECT_ROOT -- in the directory name. This allows you use this command with any nodejs project. Note,  however, that the application name ("nodejs-web-app") **is** specified in the file path.

The "stop the web app" command is worth noting because it uses some bash *magic* to find the process id (PID) and shut it down. Don't be underwhelmed; you can do some pretty amazing one-line commands using piping, grep, etc.

Components
This is the section where you specify what ia analogous to a virtual machine. Memory size, base image, ports, etc. are all configured here.

Metadata
This is required and where you define the name of the workspace. You can optionally use "generateName" instead, which specifies a prefix for a system-generated name.

Attibutes
Persistent volumes are specified here.
