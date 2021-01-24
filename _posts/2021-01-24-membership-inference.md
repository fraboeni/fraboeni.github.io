---
title: "Attacks against Machine Learning Privacy (Part 2): Membership Inference Attacks with TensorFlow Privacy"
date: 2021-01-24
excerpt: "In the second blogpost of my series about privacy attacks against machine learning models I introduce membership inference attacks and show you how to implement them with TensorFlow Privacy."
permalink: /posts/2021/01/membership-inference/
image: 2021-01-24-membership-inference.png
canonical_url: 'https://blog.franziska-boenisch.de'
header:
  teaser: 2021-01-24-membership-inference.png
tags:
  - machine learning
  - privacy
  - membership inference
  - attacks
---
<script src="//yihui.org/js/math-code.js"></script>
<!-- Just one possible MathJax CDN below. You may use others. -->
<script async
  src="//mathjax.rstudio.com/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

{% include base_path %}



Welcome to the second part of my series about attacks against machine learning (ML) privacy. 
If you haven’t checked out my last post about [model inversion attacks](/posts/2020/12/model-inversion/) yet, feel free to do so. 
It might also serve you as a little introduction about the topic of ML privacy in general. 
For today’s post I am going to assume that you have some understanding of the most common concepts in ML. 


All right, let’s get started. 
The privacy risk I am going to present today is called “membership inference”. 
We’ll first have a look on what membership inference actually means and how it can be used in order to violate individual privacy. 
Afterwards, we’ll go into some more details exploring how those attacks work on a low level. 
Then, we’ll use the TensorFlow Privacy library in order to conduct an attack on an ML classifier ourselves. 
You will see that it is pretty easy, with this very powerful tool. 
We will also (experimentally) try to verify some factors that increase a model’s vulnerability against membership inference attacks. 
Based on those, at the end, I will conclude with some words about the mitigation of the attack.

## Part 1: Membership Inference Attacks
Membership inference attacks were first described by Shokri et al. [1] in 2017. 
Since then, a lot of research has been conducted in order to make membership inference attacks more efficient, 
to measure the membership risk of a given model, and to mitigate the risks.

<figure style="width:60%;">
    <img src="{{ "/files/2021-01-24-membership-inference/pic1-membership-inference.png" | prepend: base_path }}"
     alt='machine learning workflow'/>
    <figcaption>A typical ML workflow.</figcaption>
</figure>



Let's get started with building our own model inversion: 
When you are working with tensorflow 2, the first thing to make sure is that you disable the eager execution because otherwise IBM-ART would not work. Therefore, just add the following line after your tensorflow import:
```python
import tensorflow as tf
tf.compat.v1.disable_eager_execution()
  ```
 
From IBM-ART, you mainly need to import the two following things:
```python
from art.attacks.inference import model_inversion 
from art.estimators.classification import KerasClassifier
```
The `KerasClassifier` is a wrapper for your `tf.keras` model in order to be used by the attacks. Apart from this, the workflow is pretty similar as every other ML workflow.

First, we need to specify a model architecture. I chose for a simple ConvNet architecture, but you are, of course, not limited to that.
```python
def make_model():
  """ Define a Keras model"""
  model = tf.keras.Sequential([
      tf.keras.layers.Conv2D(16, 8,
                              strides=2,
                              padding='same',
                              activation='relu',
                              input_shape=(28, 28, 1)),
      tf.keras.layers.MaxPool2D(2, 1),
      tf.keras.layers.Conv2D(32, 4,
                              strides=2,
                              padding='valid',
                              activation='relu'),
      tf.keras.layers.MaxPool2D(2, 1),
      tf.keras.layers.Flatten(),
      tf.keras.layers.Dense(32, activation='relu'),
      tf.keras.layers.Dense(10, activation='softmax')
  ])
  return model
```
After you've built the model, you can compile it with parameters of your choice:

```python
model = make_model()
optimizer = tf.keras.optimizers.SGD(learning_rate=0.1)
loss = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
model.compile(optimizer=optimizer, loss=loss, metrics=['accuracy'])
```

Then, before training on MNIST training data and labels that I stored in the variables `train_data` and `train_labels` after preprocessing, you need to put the model into the wrapper:
```python
classifier = KerasClassifier(model=model, clip_values=(0, 1), use_logits=False)
classifier.fit(train_data, train_labels,
           batch_size=264, nb_epochs=10)
```

Once the model is trained, we can start attacking it.
```python
my_attack = model_inversion.MIFace(classifier)
```

The model inverson attack in the IBM-ART offers you to specify arrays $x$ and $y$. $y$ contains class labels for the classes to be attacked. $x$ contains the initial input to the classifier under attack for each class label. (This corresponds to $x_0$ in our algorithm above.) When $x$ is not specified, a zero array is used as an initial input to the classifier for inversion.

I ran the experiment with different numbers of training epochs and this is the result:
<figure style="width:40%;">
    <img src="{{ "/files/2020-12-22-blog-post-00/restored_1.png" | prepend: base_path }}"
     alt='model inversion attack results after training one epoch'/>
    <figcaption>1 epoch of training: Restored training data class representations through model inversion.</figcaption>
</figure>
<figure style="width:40%;">
    <img src="{{ "/files/2020-12-22-blog-post-00/restored_10.png" | prepend: base_path }}"
     alt='model inversion attack results after training ten epochs'/>
    <figcaption>10 epochs of training: Restored training data class representations through model inversion.</figcaption>
</figure>
<figure style="width:40%;">
    <img src="{{ "/files/2020-12-22-blog-post-00/restored_100.png" | prepend: base_path }}"
     alt='model inversion attack results after training 100 epoche'/>
    <figcaption>100 epochs of training: Restored training data class representations through model inversion.</figcaption>
</figure>

*Note:* The data that is returned by the model inversion attack somehow is an average representation of the data that belongs to the specific classes. In the presented setting, it does not allow for an inversion of individual training data points. In the Fredrikson example, however, every individual within the face classifier represents their own class. Therefore, the attack can be used in order to retrieve information about individuals and break their privacy. 

It turns out that especially when the classifier is trained only for one epoch, many of the inversed digit representations are somehow recognizable.
I hope that this example was useful for you in order to understand how simply your ML models can be attacked nowadays, and how easily you can implement privacy attacks with help of the right tools.

If you have any questions, comments, suggestions, or corrections, please feel free to get in touch.





### Further Reading
\[1\] Shokri, Reza, Marco Stronati, Congzheng Song, and Vitaly Shmatikov. "Membership inference attacks against machine learning models." In 2017 IEEE Symposium on Security and Privacy (SP), pp. 3-18. IEEE, 2017.

\[2\] 
