---
title: "Qualifying Exam: An update on my PhD project and plans"
date: 22-08-2025 00:00 CET
modified: 19-09-2025 14:52 CET
tags: [PhD, AI, classification, taxonomy, entomology, biodiversity]
description: A summary of my qualifying exam (midterm) and status report 
image: "/qualifying-phd-exam/moths_circled_thumbnail.webp"
usemathjax: true
---

# A teaser
Below are some hand-picked excerpts from my qualifying exam --- that I passed!&nbsp; 🥳🎉
> (If you're intrigued my full progress report contains a lot more details and is available at the bottom of this page)

# Major projects in the first half of my PhD
* **Detection & segmentation (`flatbug`)**\\
  Scale- and size-agnostic inference with mask-level outputs; trained on **$$113,550$$** annotated arthropods across **$$23$$** subdatasets and **$$6,131$$** images. Generalizes with an average relative F1 drop of **$$\approx 7.1\%$$** under stratified leave-one-out; short fine-tuning largely removes penalties.
    <figure>
        <img src="/flat-bug/pyramid_tiling_visualization.png" style="width: 75%;">
        <figcaption> <strong><code class="language-plaintext highlighter-rouge">flatbug</code></strong>'s pyramid hyper-inference in action, illustrating effective segmentation across different scales.</figcaption>
    </figure>
* **Real-world deployment (`XPRIZE Rainforest`/`ETH BiodivX`)**\\
  End-to-end laptop pipeline (detection → tracking → hierarchical classification) processed **$$\sim 30,000$$** frames and yielded **$$685,611$$** detections in **one night**, enabling rapid activity curves and richness summaries.
    <figure>
        <img src="/qualifying-phd-exam/xprize_activity_orders.webp" style="width: 50%;">
        <figcaption> <strong>Order-level activity curves</strong> in 20-minute bins over a 24-hour axis --- like a clock! --- from one of the <strong><code style="language-plaintext highlighter-rouge">ETH BiodivX</code></strong> canopy camera light trap/rafts. Each concentric circle corresponds to a specific arthropod order (labelled on both ends). </figcaption>
    </figure>
* **Hierarchical classification**\\
  Three model families to be compared --- flat, multi-label (multi-head), and hierarchical multi-layer with probability aggregation to genus/family. Evaluation includes top-K plus taxonomic distance/error.
    <figure>
        <img src="/qualifying-phd-exam/hierarchy_visualized.webp" style="width: 80%;">
        <figcaption> Conceptual diagram for the fixed-hierarchy multi-layer classification model. Each color (pink/grey/yellow) corresponds to one of three conceptual "families" (bottom row), while shades correspond to genera within each (middle row), and bars in the top row are species.</figcaption>
    </figure>



# Future plans
Over the next two years, as I finish my PhD project, I plan to continue my research on automated monitoring, with a particular focus on the classification task motivated by two key insights:

* Through my education as a biologist, particular in taxonomy, evolution and bioinformatics, it has always been clear, and only more so as time goes on, that the concept of discrete **`"species"`** is an extremely practical, but at the end of the day arbitrary, delineation which obscures the fact that all organisms are part of the same family, hence all organisms are better viewed as placed in a shared "evolutionary space". Species then, are just more or less non-intersecting contiguous partitions in this space. In some cases this evolutionary space is very "lumpy" such that clusters of individuals can be separated with high support, however in many cases this is not the case, and instead individuals form a continuum without any natural separation --- this is of course also the case for the entire space if we include all individuals that have existed since **LUCA**.
* All attempts at species image classification using computer vision and deep learning so far have at the end of the day relied on species, with almost all methods treating classification as a, well, *"classification problem"*, when as I just described, the real problem isn't to tell which species an individual in an image belongs to, but rather where in the evolutionary space the individual is located --- seemingly a *"regresssion problem"*?!\\
  <div style="padding-left: 5%; width: 90%; font-size: 0.75rem; text-align: center;"><i>I am aware that some groups have used contrastive learning approaches — e.g. BioCLIP — however the contrastive space is based on human language descriptions of organisms, in particular using "the Linnean Taxonomy"; i.e. using discrete species!</i></div> 

This naturally brings up the question:
> Can we change the training objective for species image classification deep learning models from **classification** to **mapping** --- in other words where in the evolutionary landscape does the imaged individual belong? 

And the hypothesis:
> If species is an arbitrary concept, and models are trained to classify individuals as if they are instances of discrete entities, when they are not, training models for **a different objective**, one which is not rooted in arbitrary delineations, **should increase stability**, "true" learning and **generalization**.

# Status report

<embed src="{{ site.url }}{{ site.baseurl }}/assets/pdf/PhD_Progress_Report.pdf" type="application/pdf" style="width: 100%; aspect-ratio: 1;">
