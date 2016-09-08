## Install pip and dependencies

```
sudo apt-get install python-pip python-dev
```

## Install TensorFlow

```
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0-cp27-none-linux_x86_64.whl
sudo pip install --upgrade $TF_BINARY_URL
sudo pip install jupyter
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
