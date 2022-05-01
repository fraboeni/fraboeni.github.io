---
permalink: /
title: "Home"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Hello and welcome to my website. My name is Franziska Boenisch and I'm a research associate at Fraunhofer AISEC (Applied and Integrated Security). At the same time, I am pursuing a PhD at Freie Universität Berlin.

# News
I am excited to organize a workshop on Trustworthy Artificial Intelligence in Science and Society the fall at the INFORMATIK2022 conference. We are looking forward to your [submissions](https://easychair.org/cfp/trustworthy-ai-2022).

# Research
My research focus lies at the intersection of *Trustworthy Machine Learning* (ML) and *Privacy*. 

Research has shown that trained ML models do not necessarily provide privacy for the underlying training datasets, as some attacks allow to restore (aspects of) the training data from the model parameters (e.g. [model inversion attacks](/posts/2020/12/model-inversion/)), or others allow to find out if a specific data point was included in the training dataset or not ([membership inference attacks](/posts/2021/01/membership-inference/)). Both can be harmful for the privacy of the individuals whose data is represented in the training dataset.
Therefore, protecting privacy in ML models is a crucial task. I’m currently mainly researching in the area of [*Differential Privacy*](/posts/2021/03/differential-privacy/), a mathematical framework that provides formal privacy guarantees. I'm also looking into the practical evaluation of privacy loss and into the identification of potential sources for privacy leakage in privacy preserving technologies. Identifying such pain points allows us to develop a better understanding on why practical privacy stays behind the strong theoretical guarantees. This helps in adapting and extending theoretical frameworks, their implementations and their integration into real-worlds systems for enhanced privacy in practice.

Furthermore, I am investigating the impact that ML privacy has on other aspects of trustworthy ML, such as [robustness](https://arxiv.org/pdf/2105.07985.pdf), fairness, and biases.
So far, research suggests that training with privacy guarantees has a negative impact on such other desirable properties of ML models.
Therefore, I consider it of high importance to study the different aspects together in order to build an understanding on the reasons behind negative inferences.
By then developing methods that jointly optimize for different aspects, I believe that we will be able to deploy more trustworthy and private ML systems.



If you are interested in the activities of the *PrivML* research group I am building up and am coordinating, check out the tab [Research Group](https://fraboeni.github.io/research_group/). 

