- [Home](README.md)
- [Git Tutorial](git.md)

1. Go to [Docker](https://www.docker.com/get-started) and download and install Docker Desktop.

    - note that Docker Desktop needs to run from a place where it has access to admin (Windows) or root (Mac/Linux) privileges.
    - we haven't tried the download from the Linux/WSL-2 environment - but wherever you install it, be sure you select the option to let it run with WSL if you're on Windows.

2. Docker Desktop will run on startup, and then can be accessed via the desktop gui or via the command line.  If you want to be sure that Docker is installed correctly, you can run this command from the command line.

```
$ docker run -d -p 80:80 docker/getting-started

```




