- [Home](README.md)
- [Docker Tutorial](docker.md)

# Preliminaries

1. Sign up on [github](http://github.com) with a username and password if you have not already done so.<br/>

2. [Install WSL-2 for Windows](https://docs.microsoft.com/en-us/windows/wsl/install-win10) if you have not already done so. You need a certain version of Windows compiled to do this. Check the settings in Windows according to the instructions.<br/>

3. Install the [Debian Shell](https://docs.docker.com/docker-for-windows/wsl/#develop-with-docker-and-wsl-2) if you are on Windows and have not already done so.<br/>

    - if you go through this as a manual process, you'll be directed to the windows store to download a linux version.  We're using Debian for our project. Please pick this one.<br/>

    - running Docker requires elevated privileges (root) on your machine.  In Mac and Linux world, this is easy, but Windows can make it hard.  You will need to get familiar with running i.e. powershell as an admin.<br/>

    - one of the silliest but most pervasive problems with Windows is that it really really wants to use CRLF line endings (carriage return + line feed) rather than LF (line feed).  VS Code has a handy feature on the bottom right of any window that lets you change line endings easily.  You may have to use it.  :slightly_smiling_face:<br/>

    - Once you are done, you will see this on your task bar:
    ![Notice the Red Debian Icon on the Windows TaskBar](/assets/images/DebianToolBar.PNG)
    and this is your window:
    ![Looks just like a command window](/assets/images/DebianShell.PNG)<br/>

4. [Install git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). If on Windows, install from the Debian shell window.<br/>

5. Add your user credentials that you supplied to git to sign up.
```
$ git config --global user.name "Your Name Comes Here"
$ git config --global user.email you@yourdomain.example.com
```
<br/>

6. Make a directory where you want to add source code. I call mine "src".
```
$ mkdir src
$ cd src
```
<br/>

7. Clone the colrc-v2 repo (hasura branch) in your "src" directory.
```
$ git clone --branch hasura https://github.com/arizona-linguistics/colrc-v2.git
```
<br/>

8. [Install vscode](https://code.visualstudio.com/download).<br/>

    - Note that you should install this in Debian. In order to do that you can do this:
    ```
    $ cd colrc-v2
    $ code .
    ```
    <br/>
    After this, you may be prompted to install some code. Just follow the prompts.<br/>

    - You should see a window that looks like this:
    ![Looks just like a command window](/assets/images/vscode-colrc-v2.png)<br/>

9. [Install docker](docker.md), if not installed.<br/>
    - As a reminder, start the repo (as a daemonized process, with the -d flag) with:
    ```
    $ docker-compose up -d
    ```
    <br/>
    - Stop the repo with:
    ```
    $ docker-compose down
    OR press Ctrl-C if not daemonized
    ```
    </br>
    Please follow the instructions in the docker tab linked above.</br>

# Working with git

1. Using the vscode editor (code in Debian), edit a file or files of your choice. You should see the running container adapt to your changes, or throw errors if the code will not `compile`. This code in development is automatically compiled by a `cross-compiler` called `Babel`. In production, the code will be cross-compiled and the resulting javascript will be placed in a directory that the `nginx` web server will server it up from.<br/>

2. In the root directory of the project, `colrc-v2`, type this command:
```
$ git status
```
<br/>
After which you should see something like this:
![git status](/assets/images/GitStatus.PNG)<br/>
