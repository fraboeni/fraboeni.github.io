---
title: "Attacks against Machine Learning Privacy (Part 3): How to measure Membership Privacy in Machine Learning?"
date: 2020-04-24
excerpt: "In this post of my series about privacy attacks against machine learning models, I would like to discuss potential ways of measuring membership privacy in an ML model." 
permalink: /posts/2021/04/measure-membership-privacy/
image: 2021-04-24-measure-membership-privacy.png
canonical_url: 'https://blog.franziska-boenisch.de'
header:
  teaser: 2021-04-24-measure-membership-privacy.png
tags:
  - machine learning
  - privacy
  - membership privacy
  - attacks
  - quantification
---
<script src="//yihui.org/js/math-code.js"></script>
<!-- Just one possible MathJax CDN below. You may use others. -->
<script async
  src="//mathjax.rstudio.com/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

{% include base_path %}


<figure style="width:60%;">
    <img src="{{ "/files/2020-12-22-blog-post-00/01_ML-workflows.png" | prepend: base_path }}"
     alt='machine learning workflow'/>
    <figcaption>A typical ML workflow.</figcaption>
</figure>



## Part 3: Implementing a Model Inversion Attack


### Further Reading
\[1\] Fredrikson, Matt, Somesh Jha, and Thomas Ristenpart. "Model inversion attacks that exploit confidence information and basic countermeasures." In Proceedings of the 22nd ACM SIGSAC Conference on Computer and Communications Security, pp. 1322-1333. 2015.

\[2\] Nicolae, Maria-Irina, Mathieu Sinn, Minh Ngoc Tran, Beat Buesser, Ambrish Rawat, Martin Wistuba, Valentina Zantedeschi et al. "Adversarial Robustness Toolbox v1. 0.0." arXiv preprint arXiv:1807.01069(2018).
