- [Home](README.md)
- [Git Tutorial](git.md)

1. Go to [Docker](https://www.docker.com/get-started) and download and install Docker Desktop.

    - note that Docker Desktop needs to run from a place where it has access to admin (Windows) or root (Mac/Linux) privileges.
    - we haven't tried the download from the Linux/WSL-2 environment - but wherever you install it, be sure you select the option to let it run with WSL if you're on Windows.

2. Docker Desktop will run on startup, and then can be accessed via the desktop gui or via the command line.  If you want to be sure that Docker is installed correctly, you can run this command from the command line.

```
$ docker run -d -p 80:80 docker/getting-started

```

3. Once you've git cloned our colrc-v2 repo, at the command line, navigate into the folder colrc-v2 and use this command to launch our dev environment.  

```
$ docker-compose up

```

This will start the first build of the repo on your machine.  It will take some time to build, because it's doing a lot!  But after the first build, it'll be much quicker.  There will also be a lot of little messages that fly past you on screen.  As long as none of them say 'ERROR exited with code 1' or similar, it's all good. 

4. At the end of a successful up, you'll see the following stuff:

` 
colrc-v2-frontend | Search for the keywords to learn more about each warning.
colrc-v2-frontend | To ignore, add // eslint-disable-next-line to the line before.

`
5.  In your docker desktop app, you'll see one entry under `Containers / Apps`, and it'll be called `colrc-v2`, and it'll be listed as 'running'.  You'll also see at least the following images:

    - colrc-v2_frontend
    - colrc-v2_nginx
    - colrc-v2_backend
    - postgres
    - hasura/graphql-engine

6.  Point your web browser to localhost:3000 and you'll see the front page of our app.

7.  from your command line, you can now type the command to launch VSCode  

```
$ code .

```

and you'll be able to access and edit files in all of these above components in the repo.  Docker supports hot-reloading, meaning that if you change files in the repo, you'll see your browser refresh and you'll see your changes locally. 

8.  To exit, type this at the command line:

```
$ docker-compose down

```
This will stop the container, but it won't destroy the images.  They'll still be available for the next time you `docker-compose up`!
