---
title: The first post... has a very long title for testing purposes. This is not generally a great idea, but I need to test some things out.
date: 11-11-2024 16:35 CET
modified: 11-11-2024 17:51 CET
tags: [jekyll, webpage, test]
description: This is simply a sample post, to test how the layout works with posts.
image: "/first-post/wrench.png"
usemathjax: true
---

This is a sample post, to test how the layout of my webpage works with posts. 

# A post might include an image:

<figure>
    <img src="/first-post/wrench.png">
    <figcaption> This is a figure - and a caption!</figcaption>
</figure>

# A bunch of text... 

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean id diam quis diam bibendum porta. Cras tellus dolor, condimentum ut dapibus ut, dignissim mattis elit. Nullam mattis nunc in ante lobortis ullamcorper. Phasellus accumsan urna non viverra varius. Sed elementum urna eget velit varius ultrices. Nunc ac sapien ut massa vulputate consequat vitae vel lorem. 

Proin nulla mauris, dapibus in rhoncus sed, pellentesque nec nibh. Donec vulputate justo a ante condimentum, sit amet vehicula justo fermentum. Cras sit amet massa a ex iaculis tincidunt. Nulla ullamcorper rhoncus iaculis. In hac habitasse platea dictumst. Morbi eu ligula eget mi maximus sodales et at nunc. Integer feugiat purus eu egestas elementum. Vestibulum molestie justo nec odio cursus, eu sodales quam aliquet. Donec auctor nulla nec dolor lacinia dapibus. Maecenas pharetra sit amet orci non gravida.

# a table...

|----------|-------------|---------|
| **Some** | **Columns** | **...** |
|----------|-------------|---------|
| Tables   |             |         |
|          | are         |         |
|          |             | awesome |
|----------|-------------|---------|

# and some math!

1. Select one or more hidden layers, \\(L_{\text{reg}}\\), in the DNN architecture to regularize.

2. For a given minibatch of \\(n\\) inputs, perform a forward pass for each input, \\(i\\), and store the activations, \\(\mathbf{A}\\), of the chosen layers, \\(L_{\text{reg}}\\).

3. Calculate a batch activation kernel matrix, \\(\mathbf{K_{\mathrm{batch}}}\\), given a commutative kernel, \\(\omega_B(\mathbf{A_j}, \mathbf{A_k}) \rightarrow \mathcal{R}_{[0,\,1]}\\), computed between all pairs, \\(j,k\\), of the \\(n\\) inputs. Specifically, the inner product is proposed as the kernel:

    $$
    \mathbf{K}_{\mathrm{batch}, jk} = \left\langle \mathbf{A}_j, \mathbf{A}_k \right\rangle
    $$

    To ensure non-negativity, the following modification is applied:

    $$\mathbf{K}_{\mathrm{batch}, jk} = \frac{2 - \left(\langle \widehat{\mathbf{A}_j}, \widehat{\mathbf{A}_k} \rangle + 1\right)}{2}$$

    Consequently, \\(\mathbf{K_\mathrm{batch}} \in \mathcal{R}_{[0, 1]}^{n \times n}\\), simplifying further analyses. Efficient computation is as follows:

    $$\mathbf{K}_{\mathrm{batch}} = \frac{1}{2} - \frac{\widehat{\mathbf{A}} \cdot \widehat{\mathbf{A}}^\mathrm{T}}{2}$$
    
    A downside is that this kernel is scale-invariant, so other kernels might be more appropriate. A few suggestions are the Euclidean distance:
    
    $$\mathbf{K}_{\mathrm{batch}, jk} = \lVert \mathbf{A}_j, \mathbf{A}_k \rVert^2$$
    
    which unfortunately does not conform to \\(\mathcal{R}_{[0, 1]}\\) but instead \\(\mathcal{R}^+\\), or the Radial Basis Function:

    $$\mathbf{K}_{\mathrm{batch}, jk} = 1 - \exp{\left(-\frac{\lVert \mathbf{A}_j, \mathbf{A}_k \rVert^2}{\sigma^2}\right)}$$

4. The expected batch activation kernel matrix is based on the kernel structure for items \\(i\\), defined by their classes \\(C_i\\) and the class structure \\(S_C\\):

    $$E(\mathbf{K}_{\mathrm{batch}, jk}; \mathbf{C}, S_C) = \omega_s(\mathbf{C}_j, \mathbf{C}_k;\; S_C)$$

    I will call this the batch structure kernel matrix:

    $$\mathbf{K}_{\mathrm{struct}} = E(\mathbf{K}_{\mathrm{batch}}; \mathbf{C}, S_C)$$

5. Compute a "class structure" loss function, \\(\mathcal{L}_{S(i, S_C)}\\), and incorporate it into the regular loss:

    $$
    \begin{align*}
        \mathcal{L}^* &= \mathcal{L}(i) + \lambda\mathcal{L}_S(\mathbf{C}, \mathbf{A}; S_C) \\
        \mathcal{L}_S(i) &= \frac{\lVert \mathbf{K}_{\mathrm{struct}}(\mathbf{C}; S_C) - \mathbf{K}_{\mathrm{batch}}(\mathbf{A}) \rVert_F}{n^2 - n}
    \end{align*}
    $$

    Where \\(\lambda\\) is a scaling factor for the regularization term, and \\(\mathbf{A}\\) is the stacked activations of \\(L_{reg}\\) given an input batch and \\(\mathbf{C}\\) are the labels of the batch.

6. For multiple class structures, a loss is calculated separately for each structure, and each is added to the total loss. 
    
    **Note**: \\(\mathbf{K_\mathrm{batch}}\\) only needs to be computed once, so only step **[5]** must be recomputed (if \\(\mathbf{K_\mathrm{struct}}\\) is cached efficiently).