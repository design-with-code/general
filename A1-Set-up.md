# Setup

So far, we didn't require any additional setup for our projects. It was sufficient to take a text editor and the local file system and then to open the ``index.html`` in your browser by double-clicking. As we are now starting to use multiple files, we will need to set up a local web server that serves the files to avoid security violation that will prevent the application from running. 

## Development Environment: VSCode

I recommend you to install [Visual Studio Code (VSCode)](https://code.visualstudio.com) from Microsoft as editor. This is the defacto standard development environment for most developers today and offers an extensions marketplace. If you decide to use VSCode, you should also install the "SAP Fiori Tools - Extension Pack" that bundles a lot of useful tools to support your work (e.g. code completion).

## JavaScript Runtime: Node

You should also install [Node.js](https://nodejs.org), which is a JavaScript runtime environment that comes with an own package manager "Node Package Manager (NPM)" that you can use to install additional libraries. You don't need it to run the SAPUI5 prototypes and you can decide to skip this step. But if you want to use the the web server I recommend in the next step, you will need to have Node installed.

## Web Server: HTTP-Server

There are many lightweight web servers available. However, you should be aware that having a web server running on your machine is a potential security risk. Therefore, you should only run the server while you really need it for your development and you should limit it's availability to the folder that contains your files. 

For this reason, I recommend using "HTTP Server" which you can download using the Node Package Manager mentioned above and which you can esily start from the command line in VSCode. 

You should always start VSCode by opening the folder that contains your project files using ``File -> Open Folder...``. You can then open a terminal window using ``Terminal -> New Window``, which will open a new terminal window at the bottom of the VSCode window. By default, the terminal will already be in the folder you chose to open.

First you should check if you have properly installed Node.js by typing the following command into the terminal:

```bash
node -v
```

This should return a version number if installation is correct. Then you need to make sure you have currently administration rights on you machine (if you are on a company machine you might need to actively request permissions) before you try to install the ``http-server`` packages:

```bash
sudo npm install -g http-server
```

You will be asked to enter your computer password to run the command as super user (sudo). Otherwise, installation will fail due to missing permissions. Once the installation is completed, you should be able to start the server by entering:

```bash
http-server -c-1 -p 3021
```

You should get the confirmation that the server is running on 127.0.0.1:3021 (change the port according to your needs using the ``-p`` argument) and that the cache is disabled (using ``-c-1``). You can now point your browser to this URL ([``http://127.0.0.1:3021``](http://127.0.0.1:3021)) to see the contents of the current folder. In case the folder contains an ``index.html`` the browser will open this directly. In the terminal, you will see how the browser requests the individual files used by the application.


