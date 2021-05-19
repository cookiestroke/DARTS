# DARTS

**Learning about The Key Approaches used In Prior Work for Neural Architecture Search and Implementing DARTS**


1. We observe the effect of the network size on the DARTS architecture. The code used to generate the DARTS architecture is given [here](https://github.com/dragen1860/DARTS-PyTorch). To run exponentiated gradient, replace the ```arch.py``` file with the one in this repo. We have modified the step function to use exponentiated gradient descent in the ```arch.py``` file. 

We use the command 
<pre>
python train_search.py --layers <b><i>number of layers</i></b> --seed <b><i>value</i></b> 
</pre>
to search for the architecture for a model that has the required values for seed and layers. The architectures are given below.

**Seed** | **Normal convolution cell** | **Reduction convolution cell** 
--- | --- | --- 
2 | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/2normal-1.jpg) | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/2reduction-1.jpg)
9 | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/9normal-1.jpg) | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/9reduction-1.jpg) 
50 | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/50normal-1.jpg) | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/50reduction-1.jpg) 
749 | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/749normal-1.jpg) | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/749reduction-1.jpg) 

Now we will train the architectures using the command
<pre>
python train.py --cutout --auxiliary --epochs <b><i>value</i></b> 
</pre>

And then test the generated model using command

<pre>
python test.py --exp_path <b><i>path of pretrained model</i></b> 
</pre>

First we train 4 different seed value at 100 epochs and select the seed value which has the highest testing accuracy.

**Seed** | **Train Accuracy** | **Validation Accuracy** | **Test Accuracy**
--- | --- | --- | ---
2 | 94.693997 | 96.039998 | 96.109999
9 | 94.807998 | 95.919997 | 95.879999
50 | 94.625998 | 95.649998 | 95.679999
749 | 94.175997 | 95.689997 | 95.659999

We visualize the accuracies of seed values below

![text](https://github.com/cookiestroke/DARTS/blob/868e7155bd3ba67f106725794783ed19f12f5944/seed%20results.png)

Here we can see that seed value 2 gives the highest testing accuracy. We will now further train models for different number of layers to see the changes in accuracy with respect to the number of layers.

**Layers** | **Train Accuracy** | **Validation Accuracy** | **Test Accuracy**
--- | --- | --- | ---
16 | 95.675998 | 96.089997 | 96.079999
18 | 95.229998 | 96.069997 | 96.059999
20 | 94.693997 | 96.039998 | 96.109999

2. Using exponentiated gradient descent

The architecture generated using exponentiated gradient descent is given below
**Normal convolution cell** | **Reduction convolution cell** 
--- | --- 
![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/normal-1.jpg) | ![text](https://github.com/cookiestroke/DARTS/blob/30c548030e403590a628f63fa91997d83b3ac2bd/Architecture%20Images/reduction-1.jpg)

