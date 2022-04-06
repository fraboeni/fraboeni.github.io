---
title: "When the Curious Abandon Honesty: Federated Learning Is Not Private"
collection: talks
type: "Interview"
permalink: /talks/2022-03-24-fl-privacy
venue: "Private AI Webinar"
date: 2022-02-24
location: "Virtual"
---

I gave an interview on my paper "When the Curious Abandon Honesty: Federated Learning Is Not Private" in a Webinar organized by Private AI.

Find the video [here](https://www.youtube.com/watch?v=I6CgqVQ5khs) and the original paper [here](https://arxiv.org/pdf/2112.02918.pdf)

*Abstract:* In federated learning (FL), data does not leave personal devices whenthey  are  jointly  training  a  machine  learning  model.   Instead,  thesedevices share gradients, parameters, or other model updates, with acentral  party  (e.g.,  a  company)  coordinating  the  training.   Becausedata  never  “leaves”  personal  devices,  FL  is  presented  as  privacy-preserving.   Yet,  recently it was shown that this protection is but athin facade, as even a passive attacker observing gradients can recon-struct data of individual users contributing to the protocol.In this paper,  we argue that prior workstilllargely underestimatesthe vulnerability of FL. This is because prior efforts exclusively con-sider passive attackers that are honest-but-curious.   Instead,  we in-troduce an active and dishonest attacker acting as the central party,who is able to modify the shared model’s weights before users com-pute  model  gradients.   We  call  the  modified  weightstrap  weights.Our active attacker is able to recover user dataperfectly.  Recoverycomes with near zero costs: the attack requires no complex optimiza-tion objectives.  Instead, our attacker exploits inherent data leakagefrom model gradients and simply amplifies this effect by maliciouslyaltering the weights of the shared model through the trap weights.
