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

- The files in red have not been committed.
- The branch should be `hasura` for now.
- If there are files in green, they have been committed and are waiting to be pushed.
- Any files that have been modified or added can be saved by using `git add <file>`.
- Any files that have been deleted can be removed by using `git rm <file>`.
</br>
In this case, I would type these commands:
```
$ git add .gitignore
$ git add nginx/Dockerfile
$ git rm nginx/assets/build/config/sites-enabled/default
$ git add nginx/entrypoint.sh
```
<br/>
Now typing `git status` returns this information:
![git status after adding and removing files](/assets/images/GitStatusReadyToCommit.PNG)<br/>

To commit to the repo and add a meaningful commit message, type something like this:
```
git commit -m "Ignored node_modules, removed old default site for nginx, entrypoint.sh copies audio and text files"
```
<br/>
If you try this and you haven't set your git credentials, you will see this message:
![git commit without credentials](/assets/images/GitCommitFailed.PNG)<br/>

After fixing that, you should see a success:
![git commit](/assets/images/GitCommitSuccess.PNG)<br/>

And now you should be able to push:
```
git push
```
<br/>
And you should see:
![git push](/assets/images/GitPush.PNG)<br/>
Note that you may get a message that some modules are out of compliance with security concerns. You can ignore that for now.

# Altering the frontend code

- We need two people (at least) working together and altering the code to see the potential conflicts that can arise from multiple people working on code. The plan here is:
- First of all, you want to make sure that each person has run `docker-compose up` to start the docker container.
- Person 1 checks out and changes the frontend code
![person 1 code view add](/assets/images/codeViewAdd.PNG)<br/>
![person 1 page view add](/assets/images/pageViewAdd.PNG)<br/>
- Person 2 will check out and change the frontend code
![person 2 code view add](/assets/images/codeViewAdd2.PNG)<br/>
![person 2 page view add](/assets/images/pageViewAdd2.PNG)<br/>
- Person 1 will `git add`, `git commit`, and `git push` changes to the code
- Person 2 will `git add`, `git commit`, and try to `git push` changes to the code
- Conflicts will arise. Person 2 needs to `git pull` the frontend code.
![git push fail](/assets/images/GitPushFail.PNG)<br/>
- If you can auto-merge you can use the editor to see what changed between edits
![code change diff](/assets/images/CodeChangeDiff.PNG)<br/>
- Making a change that causes conflicts will result in an editor showing the `merge conflicts`
![merge conflict code](/assets/images/mergeConflictCode.PNG)<br/>
- Now person 1 sees `merge conflicts` in the code because 2 people have edited the same file. These conflicts must be resolved. Looking in the editor shows the conflicts and how to resolve them.



![git code merge conflict](/assets/images/gitCodeMergeConflict.PNG)<br/>
![code change view](/assets/images/CodeChangeView.PNG)<br/>
![code page add auto merge](/assets/images/codePageAddAutoMerge.PNG)<br/>

![git auto merge](/assets/images/GitAutoMerge.PNG)<br/>
![fix git merge conflict push success](/assets/images/fixGitMergeConflictPushSuccess.PNG)<br/>
