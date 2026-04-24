---
title: "Long Short-Term Memory "
date: 2026-04-01
permalink: /lstms/
layout: archive
---

<script src="//yihui.org/js/math-code.js"></script>
<!-- Just one possible MathJax CDN below. You may use others. -->
<script async
  src="//mathjax.rstudio.com/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

{% include base_path %}


This page provides study materials on **Long Short-Term Memory (LSTM) networks**. To prepare the lecture, please watch the flipped classroom-style lecture video. For more auditive learners, I also included an AI-generated podcast based on the lecture. You can download all the lecture materials and study at your own speed.

To test and solidify your knowledge, I also provide a **small interactive quiz**, and a **Jupyter notebook** with a coding exercise that you can do locally. Finally, if you have questions you want to discuss during our in-person session, please submit them via the **online question form**.



## Watch the Lecture


<div style="max-width: 800px; margin: auto;">
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
<iframe width="560" height="315" src="https://www.youtube.com/embed/QGaYDW5juqU?si=nDe-jcKKIKEoLFMv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

</div>
</div>

---

## Download the Lecture Slides

📄 Please click the image to download/view the slides (PDF).

<a href="{% include base_path %}/files/2026-04-lstms/lstms-slides.pdf">
  <img src="/files/2026-04-lstms/lstms-slide.png" alt="Slides Preview" width="800" style="display:block; margin:auto;">
</a>



---

## Listen to the Podcast

Using the lecture notes, I made an AI-generated podcast with NotebookLM. 

<audio controls>
  <source src="{{ '/files/2026-04-lstms/lstms.mp3' | relative_url }}" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>



---

## Explore the Topic by Coding

I believe that any topic is best learned hands-on. Therefore, I prepared a Jupyter notebook where you can explore LSTMs by coding. My notebook provides the skeleton code which generates some training data and does the operational logic for you. You have three TASKs to fulfill based on your understanding of the material to make the network train. We will not use any abstractions like the `torch.torch.nn.LSTM`, but we will use PyTorch tensors and autograd, so we do not have to derive gradients manually. The notebook is view-only, please make an editable copy for yourself to start working.

<a href="https://colab.research.google.com/drive/1aLJu7kV5x8HJ27qn5xob4aQ6UbxUH3-p?usp=sharing" 
   target="_blank">
   <img width="200" src="https://colab.research.google.com/assets/colab-badge.svg" />
</a>


## Quiz

You can test your understanding of the lecture with this interactive quiz. The correct answers are displayed on the last page. If you got less than 7 out of the 10 questions correctly, I recommend re-watching the lecture video and/or looking into the additional study material. You can also submit any question that remains unclear in the form below.

<div data-tf-live="01KPVA6W5MRABFW85P1KQBG58H"></div>

## Submit Questions for the In-Person Session

If you have questions that you want to discuss during the in-person session, please submit them through the form.

<div style="max-width: 800px; margin: auto;">
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
<iframe src="https://docs.google.com/forms/d/e/1FAIpQLSdrRyKRrbv516NnUqf2glT4SHIZob0xHZKdseaG6SDrlXgFZw/viewform?embedded=true" width="640" height="429" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>
</div>
</div>

## Find Additional Study Materials

Find below a listing on additional study materials that might help you to get more familiar with the topic. I included both short and long references, depending on how deep of a dive you want to take into the topic. I also linked some recent research around the topic for those who are interested in the development of the field.

### Brief Dive
- Blog on [LSTMs](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- Blog with background on [RNNs](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)

### Deep Dive
- Full lecture on Simple and LSTM RNNs [(Stanford CS224N NLP)](https://www.youtube.com/watch?v=0LixFSa7yts)
- [Paper](https://www.bioinf.jku.at/publications/older/2604.pdf) introducing LSTMs 

### Going Above & Beyond: Check More Recent Research
- NeurIPS 2024 (LSTM extension): [xLSTM: Extended Long Short-Term Memory](https://proceedings.neurips.cc/paper_files/paper/2024/file/c2ce2f2701c10a2b2f2ea0bfa43cfaa3-Paper-Conference.pdf)
- NeurIPS 2017 (Transformers as a modern-day alternative to LSTMs): [Attention is all you need](https://proceedings.neurips.cc/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf)



