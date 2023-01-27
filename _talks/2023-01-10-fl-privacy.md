---
title: "What trust model is needed for federated learning to be private?"
collection: talks
type: "Invited Talk"
permalink: /talks/2023-01-10-fl-privacy
venue: "Apple"
date: 2023-01-10
location: "Virtual"
---

*Abstract:* In federated learning (FL), data does not leave personal devices when they are jointly training a machine learning model. Instead, these devices share gradients with a central party (e.g., a company). Because data never "leaves" personal devices, FL was promoted as privacy-preserving. Yet, recently it was shown that this protection is but a thin facade, as even a passive attacker observing gradients can reconstruct data of individual users. 
In this talk, I will explore the trust model required to implement practical privacy guarantees in FL by studying the protocol under the assumption of an untrusted central party. I will first show that in vanilla FL, when dealing with an untrusted central party, there is currently no way to provide meaningful privacy guarantees. I will depict how gradients of the shared model directly leak some individual training data points—and how this leakage can be amplified through small, targeted manipulations of the model weights. Thereby, the central party can directly and perfectly extract sensitive user-data at near-zero computational costs. Then, I will move on and discuss defenses that implement privacy protection in FL. Here, I will show that an actively malicious central party can still have the upper hand on privacy leakage by introducing a novel practical attack against FL protected by secure aggregation and differential privacy – currently considered the most private instantiation of the protocol. I will conclude my talk with an outlook on what it will take to achieve privacy guarantees in practice.