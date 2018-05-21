# Intel® Movidius™ NCS MNIST example

## Practice NCS using MNIST dataset with Keras

Train a simple CNN for MNIST using script

```
$ python3 train-mnist.py
```

Train a simple CNN for MNIST using jupyter

```
train-mnist.ipynb
```

Convert Keras model to Tensorflow model using script (model.json and weights.h5 file)

```
$ python3 convert-mnist.py
```

Convert Keras model to Tensorflow model using jupyter

```
convert-mnist.ipynb
```

Convert Keras model to Tensorflow model using script (model.h5 file)

```
$ python3 convert-mnist-only-h5.py
```

Convert Keras model to Tensorflow model using jupyter

```
convert-mnist-only-h5.ipynb
```

Compile MNIST model using mvNC Toolkit

```
$ mvNCCompile TF_Model/tf_model.meta -in=conv2d_1_input -on=dense_2/Softmax
```

Check, Profile  model using mvNC Toolkit

```
$ mvNCCheck TF_Model/tf_model.meta -in=conv2d_1_input -on=dense_2/Softmax
$ mvNCProfile TF_Model/tf_model.meta -in=conv2d_1_input -on=dense_2/Softmax
```

If `tensorflow.python.framework.errors_impl.InvalidArgumentError`*: You must feed a value for placeholder tensor 'conv2d_1_input' with dtype float and shape [?,28,28,1]* occur on execute command above, please edit ncsdk source in `/usr/local/bin/ncsdk/Controllers/TensorFlowParser.py` line 1059, add a feed_dict to eval:

```
# desired_shape = node.inputs[1].eval() 
desired_shape = node.inputs[1].eval(feed_dict={inputnode + ':0' : input_data}) 
```

Do prediction on a random image using NCS
if you want use mnist.load_data() provided by TF, you should remark line 2,8~11 and edit line 6
or you must install mnist from PyPi using `$pip3 install mnist` .

```
$ python3 predict-mnist-ncs.py
```

Do prediction on a random image using Keras

```
$ python3 ppredict-mnist-keras.py
```

---

model.json `Only contain model graph (Keras Format)`.

weights.h5 `Only contain model weights (Keras Format)`.

model.h5 `Both contain model graph and weights (Keras Format)`.


## Reference

+ [oraoto/learn_ml](https://github.com/oraoto/learn_ml/blob/master/ncs/README.md)
+ [ardamavi/Intel-Movidius-NCS-Keras](https://github.com/ardamavi/Intel-Movidius-NCS-Keras)
