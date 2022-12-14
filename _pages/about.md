---
permalink: /
title: "Home"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Hello and welcome to my website. My name is Franziska Boenisch and I'm a Postdoctoral Fellow at the [Vector Institute for Artificial Intelligence](https://vectorinstitute.ai/) supervised by [Prof. Dr. Nicolas Papernot](https://www.papernot.fr/). Prior to joining Vector, I was a PhD candidate at Freie University Berlin and a research assosiate at the Fraunhofer Institute for Applied and Integrated Security [(AISEC)](https://www.aisec.fraunhofer.de/en.html).


# Research
My research focus lies at the intersection of *Trustworthy Machine Learning* (ML) and *Privacy* from the perspective of individual users and data owners. 

Research has shown that trained ML models do not necessarily provide privacy for the underlying training datasets, as some attacks allow to restore (aspects of) the training data from the model parameters (e.g. [model inversion attacks](/posts/2020/12/model-inversion/)), or others allow to find out if an individual data point was included in the training dataset or not ([membership inference attacks](/posts/2021/01/membership-inference/)). Both can be harmful for the privacy of the individuals whose data is represented in the training dataset.
Therefore, protecting privacy in ML models is a crucial task. I’m currently mainly researching in the area of [*Differential Privacy*](/posts/2021/03/differential-privacy/), a mathematical framework that provides formal privacy guarantees. I'm also looking into the practical evaluation of privacy loss and into the identification of potential sources for privacy leakage in privacy preserving technologies. Identifying such pain points allows us to develop a better understanding on why practical privacy stays behind the strong theoretical guarantees. This helps in adapting and extending theoretical frameworks, their implementations and their integration into real-worlds systems for enhanced privacy in practice.

Furthermore, I am investigating the impact that ML privacy has on other aspects of trustworthy ML, such as [robustness](https://arxiv.org/pdf/2105.07985.pdf), fairness, and biases.
So far, research suggests that training with privacy guarantees has a negative impact on such other desirable properties of ML models.
Therefore, I consider it of high importance to study the different aspects together in order to build an understanding on the reasons behind negative inferences.
By then developing methods that jointly optimize for different aspects, I believe that we will be able to deploy more trustworthy and private ML systems.





# News

- **December 2022:**  Our Workshop on Trustworthy ML under Limited Data and Compute was accepted for ICLR'23. Link to CfP coming soon!
- **November 2022:**  Paper accepted for publication at PoPETs'23: [A Unified Framework for Quantifying Privacy Risk in Synthetic Data](https://arxiv.org/pdf/2211.10459.pdf).
- **September 2022:**  Paper accepted at the 36th Conference on Neural Information Processing Systems (NeurIPS'22): [Dataset Inference for Self-Supervised Models](https://arxiv.org/abs/2209.09024).
- **September 2022:** Paper accepted for publication at PoPETs'23: [Individualized PATE: Differentially Private Machine Learning with Individual Privacy Guarantees](https://arxiv.org/abs/2202.10517).
- **September 2022:** We're presenting our paper on [Introducing Model Inversion Attacks on Automatic Speaker Recognition](https://www.isca-speech.org/archive/pdfs/spsc_2022/pizzi22_spsc.pdf) at the 2nd Symposium on Security and Privacy in Speech Communication (SPSC).
- **August 2022:** I'm happy to announce that I finalized my PhD duties and will be joining the Canadian Vector Institute as a Postdoctoral Fellow under the supervision of Prof. Dr. Nicolas Papernot by the end of the month.
- **April 2022:** Super proud that my interview on Differential Privacy with the Google-Aufbruch magazine made it to the [title page](https://kstatic.googleusercontent.com/files/1791d34518d7768efe0fb6d698f45a276c507ddbb67bcc916c87c564de8fc212023df574da98c9a8d8f149dc964371e003b6120b1f2188740a464ef157102ef4).


