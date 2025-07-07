---
title: "Feature Importance in Decision Trees"
date: 2025-07-01
permalink: /trees/
layout: archive
---

<script src="//yihui.org/js/math-code.js"></script>
<!-- Just one possible MathJax CDN below. You may use others. -->
<script async
  src="//mathjax.rstudio.com/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

{% include base_path %}


This page provides study materials on decision trees and explainable AI. It introduces the intuition behind how **decision trees** work and explains how to build them using **impurity-based importance** calculations. The content also covers **feature importance** and discusses how these concepts relate to **explainable AI**.

## (Re-)Watch the Lecture

<div style="max-width: 800px; margin: auto;">
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/pVoB43A-_tI?si=Ht2OMR1pT50RvNBt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
</div>

---

## Download the Lecture Slides

📄 Please click the image to download/view the slides (PDF).

<a href="{% include base_path %}/files/2025-07-trees/lecture-slides.pdf">
  <img src="/files/2025-07-trees/trees.png" alt="Slides Preview" width="800" style="display:block; margin:auto;">
</a>



---

## Listen to the Podcast

Using the lecture notes, I made an AI-generated podcast with NotebookLM. 

<audio controls>
  <source src="/files/2025-07-trees/trees-podcast.wav" type="audio/wav">
  Your browser does not support the audio element.
</audio>

---

## Play with the Code  

The following code shows you how to use sklearn's decision trees. If you want to practice how to implement a decision tree, please check out the coding exercise I prepared in this [GitHub Repo](https://github.com/fraboeni/trees/blob/main/decision_trees_and_feature_importance.ipynb).
```python
import pandas as pd             # to have nice data frames
from sklearn import tree        # for the decision tree
import matplotlib.pyplot as plt # for plotting
import numpy as np

data = pd.read_csv("dataset_tml.csv",index_col=0)

# Map categorical features and label
data = data.replace({"Yes": 1, "No": 0}) # yes and no strings are mapped to 1 and 0

# Split into features and label
X = data.iloc[:, :-1]  # all columns except "Passed"
Y = data.iloc[:, -1]   # the "Passed" column

clf_gini = clf_gini.fit(X, Y)
clf_gini.predict(X)

# Look into the feature importance
impotances_gini = clf_gini.feature_importances_
print(impotances_gini)

# Plot the entire tree
from sklearn import tree
tree.plot_tree(clf_gini)
```

<img src="/files/2025-07-trees/final_tree.png" alt="Final Decision Tree" width="400">

## Find Additional Study Materials

1. Full [Stanford Lecture](https://www.youtube.com/watch?v=wr9gUr-eWdA) on Decision Trees
2. Small [Lecture Video](https://www.youtube.com/watch?v=_L39rN6gz7Y ) on Gini Impurity
3. Book: Pattern Recognition and Machine Learning, [Chapter 14.4](https://github.com/Benlau93/Data-Science-Curriculum/blob/master/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf)
4. Book: Interpretable Machine Learning, [Chapter 9](https://christophm.github.io/interpretable-ml-book/)
