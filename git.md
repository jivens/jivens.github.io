1. Sign up on [github](http://github.com) with a username and password if you have not already done so.
2. [Install WSL-2 for Windows](https://docs.microsoft.com/en-us/windows/wsl/install-win10) if you have not already done so. You need a certain version of Windows compiled to do this. Check the settings in Windows according to the instructions.
3. Install the [Debian Shell](https://docs.docker.com/docker-for-windows/wsl/#develop-with-docker-and-wsl-2) if you are on Windows and have not already done so.
    - if you go through this as a manual process, you'll be directed to the windows store to download a linux version.  We're using Debian for our project. Please pick this one.
    - running Docker requires elevated privileges (root) on your machine.  In Mac and Linux world, this is easy, but Windows can make it hard.  You will need to get familiar with running i.e. powershell as an admin.
    - one of the silliest but most pervasive problems with Windows is that it really really wants to use CRLF line endings (carriage return + line feed) rather than LF (line feed).  VS Code has a handy feature on the bottom right of any window that lets you change line endings easily.  You may have to use it.  :slightly_smiling_face:
4. [Install git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). If on Windows, install from the Debian shell window.
5. Add your user credentials that you supplied to git to sign up
```
$ git config --global user.name "Your Name Comes Here"
$ git config --global user.email you@yourdomain.example.com
```
6. Make a directory where you want to add source code. I call mine "src".
```
$ mkdir src
$ cd src
```
7. Clone the colrc-v2 repo (hasura branch) in your "src" directory
```
$ git clone --branch hasura https://github.com/arizona-linguistics/colrc-v2.git
```
