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
     alt='concept of membership inference attacks'/>
    <figcaption>The concept of membership inference attacks.</figcaption>
</figure>

Let’s first have a superficial look on the topic before diving deep into the algorithmic background and attack structure.

### Overview on Membership Inference Attacks
The aim of a membership inference attack is quite straight forward: Given a trained ML model and some data point, decide whether this point was part of the model’s training sample or not. If you can’t see the privacy risk of it straight away, don’t worry. But think of the following situation:

> Imagine you are in a clinical context. There, you may have an ML model that is supposed to predict an adequate medical treatment for cancer patients. This model, logically, needs to be trained on the data of cancer patients. Hence, given a data point, if you are able to find out, that it was indeed part of the model’s training data, then you know that the corresponding patient must have cancer. As a consequence, this patient’s privacy would be disclosed. 


```python
import tensorflow as tf
tf.compat.v1.disable_eager_execution()
  ```
 




### Further Reading
\[1\] Shokri, Reza, Marco Stronati, Congzheng Song, and Vitaly Shmatikov. "Membership inference attacks against machine learning models." In 2017 IEEE Symposium on Security and Privacy (SP), pp. 3-18. IEEE, 2017.

\[2\] 
