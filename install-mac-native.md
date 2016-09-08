
# Installing TensorFlow Natively on OS X

We will present the tutorial in [Jupyter](jupyter.org) notebooks.  To
run them on your machine, you will need a working TensorFlow
installation (v0.10).

Follow these instructions, which assume you have OS X (probably 10.11
"El Capitan"), and will use Python 2.7.

## Open a terminal.

Open `Terminal`. This tutorial assumes you are using `bash`, which you
probably are.

## Clone this repository

Using git, clone this tutorial and enter that directory.

```
git clone https://github.com/wolffg/tf-tutorial.git
cd tf-tutorial
```

## Install Pip and Virtualenv

Pip is a package management system used to install and manage software
packages written in Python.  Virtualenv allows you to manage multiple
package installations.

At your Terminal window, run the following commands. 
```
# Mac OS X
sudo easy_install --upgrade pip
sudo easy_install --upgrade six
sudo pip install --upgrade virtualenv
sudo pip install --upgrade protobuf
```

These should install pip, some dependencies, and Virtualenv.

Now, create a virtual environment.

```
$ virtualenv --system-site-packages ~/tensorflow
```

You will need to Activate the environment, which is to say switch your
Python enviroment to a fresh one with clean dependencies.

```
$ source ~/tensorflow/bin/activate
New python executable in /Users/wolff/tensorflow/bin/python
Installing setuptools, pip, wheel...done.
(tensorflow) $
```

You are now running in a special Python enviroment with safe
dependencies.  

Finally, Select a binary and install TensorFlow and Jupyter. For this
lab, we will use CPU-only Mac.

```
# Mac OS X, CPU only, Python 2.7:
export TF_BINARY_URL=export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-0.10.0-py2-none-any.whl
pip install --upgrade $TF_BINARY_URL
pip install --upgrade jupyter
```

## Running Jupyter

From your "tensorflow" virtualenv prompt, run the following:

```
(tensorflow) $ jupyter notebook
```

Click on `0_tf_hello_world.ipynb` to test that jupyter is running
correctly.

You should be able to run the notebook without issue.

<hr>

## Installation notes

Virtualenv is a tidy way of managing your dependencies.  Any time
you want to run TensorFlow, you can activate by `source
~/tensorflow/bin/activate`.  To exit the virtual environment, simply
type `deactivate`.

Without using Virtualenv, at this time you may run into issues with
upgrading some pre-installed Python dependencies (especially `numpy`
on MacOS El Capitan 10.11).