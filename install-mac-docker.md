
# Installing TensorFlow on Docker on a Mac.

This tutorial is presented via [Jupyter](jupyter.org) notebooks.  To
run them on your machine, you will need a working TensorFlow
installation (v0.10).

Below are instructions on how to set up a TensorFlow environment using
Docker.  Although Docker runs in a VM, the advantage is that Docker
images come with all dependencies are pre-installed and pre-compiled.

## Setup

Docker runs your notebooks from a virtual machine.  Docker images
already contain installed and compiled versions of TensorFlow.

Prerequisites:
* A Mac or Ubuntu Linux machine (Docker will work on Windows, but the step-by-step instructions here may not work perfectly since we have not tried them)
* Some knowledge of Python

If you already have the Docker Toolbox installed, skip to
"Installing/running a TensorFlow Docker Image." Otherwise, go to
[docs.docker.com/mac/](http://docs.docker.com/mac/) and follow the
instructions there, which should roughly be:

Download the Docker Toolbox. 
* On the Toolbox page, find the Mac version.
  * Download a DockerToolbox-1.xx.xx.pkg file (180MB).
  * Run that downloaded pkg to install the Toolbox.
  * At the end of the install process, choose the Docker Quickstart Terminal.
  * Open a terminal window and follow the installation script.
* If you have already installed Toolbox, just run the Docker Quickstart Terminal in `/Applications/Docker/`.
* Launch the **Docker Quickstart Terminal** 
  * This may take some time the first time to make an SSH connection.
* Run the suggested command in the terminal to confirm Docker
installation has worked:
```
docker run hello-world
```

#### Troubleshooting OS X

On OS X, you may see:

```
Error checking TLS connection: Something went wrong running an SSH command!
command : ip addr show
err     : exit status 255
```

At which point you may have to destroy and recreate your docker instance like so:

```
docker-machine rm default
docker-machine create --driver virtualbox default
```

#### Installing and Running the TensorFlow Image

On OS X, if you have not already, run the Docker Quickstart Terminal,
usually found in `/Applications/Docker`, and which looks like this:

![Quickstart Terminal Icon](images/quickstart-icon.png)

There will be a long pause as the Docker container starts and gets an
SSH keys and an IP address.

Once you see an ASCII whale in the newly-opened terminal, run this command:

```
docker run -it tensorflow/tensorflow:0.10.0rc0 bash
```

Check to see if your TensorFlow works by invoking Python from the container’s command line (you’ll see `root@xxxxxxx#`):

```
# python

import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
```

If you see "Hello, Tensorflow!", it works!

## Run Docker with Jupyter and TensorBoard

Note: On Mac OS X, if you have not already opened a **Docker
Quickstart Terminal**, you must do so now.

Go to where you cloned the repository (we're assuming `$HOME`):

```
cd $HOME
docker run  -v $HOME/tensorflow-tutorial:/tutorial -p 0.0.0.0:6006:6006 -p 0.0.0.0:8888:8888 -it tensorflow/tensorflow:0.10.0rc0 bash
```

This will start a Docker instance with the tutorial materials mounted
at `/tutorial`.

*(Note: All further commands are run in the Docker
image, so your prompt will be `root@[something]#`).*

Once started, run the Jupyter server in the right directory.

```
cd /tutorial
/run_jupyter.sh &
```

You will also want to run TensorBoard:

```
tensorboard --logdir=`pwd` &
```

**On OSX:** You can navigate to:

* [http://192.168.100.99:8888](http://192.168.100.99:8888)

or whichever local address your VM has on your machine.

TensorBoard is available in a similar place, either [http://localhost:6006](http://localhost:6006) or
[http://192.168.100.99:6006](http://192.168.100.99:6006) on MacOS.

On OS X, you can find the exact address under the whale where you
started your terminal, shown here:

![Docker whale image](images/docker-whale.png)

## When You're Done

To exit Docker, you can simply enter `exit` or hit `Ctrl-D`.
