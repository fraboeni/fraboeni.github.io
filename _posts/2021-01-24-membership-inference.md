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
Membership inference attacks were first described by Shokri et al. \[1\] in 2017. 
Since then, a lot of research has been conducted in order to make membership inference attacks more efficient, 
to measure the membership risk of a given model, and to mitigate the risks.

<figure style="width:60%;">
    <img src="{{ "/files/2021-01-24-membership-inference/pic1-membership-inference.png" | prepend: base_path }}"
     alt='concept of membership inference attacks'/>
    <figcaption>The concept of membership inference attacks.</figcaption>
</figure>

Let’s first have a superficial look on the topic before diving deep into the algorithmic background and attack structure.

### Overview on Membership Inference Attacks
The aim of a membership inference attack is quite straight forward: Given a trained ML model and some data point, decide whether this point was part of the model’s training sample or not. If you can’t see the privacy risk of it straight away, don’t worry. But think of the following situation:

> Imagine you are in a clinical context. There, you may have an ML model that is supposed to predict an adequate medical treatment for cancer patients. This model, logically, needs to be trained on the data of cancer patients. Hence, given a data point, if you are able to find out, that it was indeed part of the model’s training data, then you know that the corresponding patient must have cancer. As a consequence, this patient’s privacy would be disclosed. 

I hope that with this example I could convince you of the importance of membership privacy. Basically in any context where the sheer fact of being included in a sample can be privacy disclosing, membership inference attacks pose a severe risk.


### How do Membership Inference Attacks Work?
Most membership inference attacks work similar as the original example described by Shokri et al. \[1\], namely by building a binary meta-classifier $f_{attack}$ that, given a model $f$ and a data point $x_i$, decides whether or not $x_i$ was part of the model’s training sample $X$.

<figure style="width:60%;">
    <img src="{{ "/files/2021-01-24-membership-inference/pic2-meta-classifier.png" | prepend: base_path }}"
     alt='how do membership inference attacks work'/>
    <figcaption>The basic idea on how to perform membership inference attacks.</figcaption>
</figure>

In order to train this meta-classifier $f_{attack}$, $k$*shadow models* $f_{shaddow}^j$  are constructed. 
Those models are supposed to imitate the behaviour of the original ML model $f$. 
However, their training data $X’$, i.e. the ground truth $y’$ for the binary classifications, is known to the attacker. 

By using the knowledge about the shadow models’ training data, input output-pairs $(x’_i, f_{shaddow}^j; y’_i)$ for the meta-classifier can be constructed, 
such that it learns the task of distinguishing between members and non-members based on an ML model’s behavior on them.

<figure style="width:60%;">
    <img src="{{ "/files/2021-01-24-membership-inference/pic3-meta-classifier-training.png" | prepend: base_path }}"
     alt='training of a meta classifier that is able to perfom membership inference attacks'/>
    <figcaption>The training of a meta classifier that is able to perform membership inference attacks.</figcaption>
</figure>

In this process, Shokri et al. \[1\] claim that the more shadow models, the more accurate the attack will be. 
The authors also describe several methods for creating $X’$, e.g. based on noisy real-world data that is similar to the original $X$, 
or based on data synthetization with help of $f$ or statistics over $X$. 
They showed that with this setting, a membership inference attack can even be trained with only black-box access to the target model and without any prior knowledge about its training data.

## Implementing Membership Inference Attacks 
There are several tools for implementing membership inference attacks. The two that I am most familiar with are the IBM-ART framework that I used in [my last blogpost](/posts/2020/12/model-inversion/) in order to implement model inversion attacks, and [TensorFlow Privacy’s Memberhip Inference]( https://github.com/tensorflow/privacy/tree/master/tensorflow_privacy/privacy/membership_inference_attack). For my purposes (mainly trying to quantify privacy of a given model), so far, the TensorFlow version has proven more useful, as on my use cases, the attacks were more successful. 
Therefore, we are going to look on an implementation of membership inference attacks with TensorFlow Privacy in the following. 

### TensorFlow Privacy’s Membership Inference-Framework
In my opinion, the usability of TensorFlow Privacy’s Membership Inference attack has had its ups and downs in the last months. For a long time, TensorFlow Privacy used to work with TensorFlow version 1 only. For me, this included a lot of hassle by continuously changing between virtual environments with TensorFlow version 1 and 2 in order to take the maximum capabilities out of both. 
Then, by the end of 2020, TensorFlow Privacy was successfully updated to work with Tensorflow 2. I was all excited, and happy. 
However, in my opinion, there is still some struggle ongoing if you want to include the membership inference attacks into longer-lasting projects: For example, if I am not mistaken, the interface of TensorFlow Privacy’s membership inference has been updated and changed completely WITHOUT a version number increase so far (stayed 0.5.1 all along). So, don’t be confused if your package 0.5.1 has entirely different code that the one that you find in the online repo, or if you can’t get your old code to run. 
In order to stay always up to date, the helpful community suggested to me to use the following 
```
!pip install -U git+https://github.com/tensorflow/privacy
```
and it works.

Apart from these issues that might decrease in the future, I find TensorFlow Privacy to be a really useful tool for many purposes, one of it being the implementations of membership inference attacks.

### Implementing a Membership Inference Attack with TensorFlow Privacy
When evaluating membership inference risks, I prefer to work with the CIFAR10 dataset instead of MNIST because, according to my experience, the membership privacy risk of simple models trained with MNIST is usually already quite low. 
Therefore, one barely sees any changes when using measures to try mitigating membership privacy risks.

For those of you who are not familiar with the [CIFAR10 dataset]( https://www.cs.toronto.edu/~kriz/cifar.html): it’s another dataset that you can directly load through keras:
```python
train, test = tf.keras.datasets.cifar10.load_data()
```
It consists of 60000 32x32 colour images in 10 classes, with 6000 images per class (50000 training images and 10000 test images). The classes are airplane, automobile, bird, cat, deer, dog, frog, horse, ship, and truck.

<figure style="width:60%;">
    <img src="{{ "/files/2021-01-24-membership-inference/pic4-cifar10-data-examples.png" | prepend: base_path }}"
     alt='example images of the CIFAR10 dataset'/>
    <figcaption>Example images of the CIFAR10 dataset.</figcaption>
</figure>

```python
import tensorflow as tf
tf.compat.v1.disable_eager_execution()
  ```
 




### Further Reading
\[1\] Shokri, Reza, Marco Stronati, Congzheng Song, and Vitaly Shmatikov. "Membership inference attacks against machine learning models." In 2017 IEEE Symposium on Security and Privacy (SP), pp. 3-18. IEEE, 2017.

\[2\] 
