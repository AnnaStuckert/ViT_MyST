---
title: Introduction 🧙
short_title: test
authors:
  - name: Anna Stuckert
    affiliations:
      - University of St Andrews
    email: anna.stuckert97@gmail.com
    corresponding: true
    orcid: 0000-0003-3737-0972
    url: https://annastuckert.github.io
abstract: |
  ViT_Facemap is a project that utilizes Vision Transformers (ViT) for facial mapping. The project is primarily focused on the development and application of advanced machine learning models to detect and interpret facial features using ViT architectures. 
exports:
  - format: tex
    template: volcanica
    article_type: Report
    output: arxiv.zip
# - format: pdf
#   template: volcanica
#   article_type: Report
---


## Machine Learning in Emotional Expression Analysis

Facial expressions in mice can be used as a reliable indicators of emotional states and corresponding
neural activity [](doi:10.1126/science.aaz9468). Recently, the resurgence of interest in facial expression analysis is motivated by the significant advancements within the area of deep learning [](doi:10.1038/nature14539). An important aspect of facial expression analysis is the ability to accurately track multiple orofacial key
points. Previously, humans or animals have been marked with e.g. reflective markers to assist computer-based tracking, but a substantial advancement in behaviour tracking was achieved with the development of DeepLabCut (DLC). DLC is an efficient method for markerless pose estimation. It is based on deep neural networks and transfer learning, and it is able to achieve human-level accuracy with minimal training data [](doi:10.1038/s41593-018-0209-y). Additionally, FACEMAP is a recently introduced tracking tool for mouse orofacial movements, exhibiting performance comparable to human-level accuracy [](doi:10.1038/s41593-023-01490-6).
Changes in position of facial features can be used for discriminating facial expressions apparent under varying circumstances. In the study by Dolensek and colleagues, the features of the images of
the mouse facial expressions upon different types of emotional stimuli are extracted using a Histogram of Oriented Gradients (HOG) to assess similarity, and a random forest classifier is trained and able to
predict the type of stimulation based on the facial expression with high accuracy [](doi:10.1126/science.aaz9468). In another study investigating detection of facial expressions associated with pain, two deep
convolutional neural networks (CNNs) are employed to discern mouse facial expressions and
investigate the presence or absence of post-surgical and/or post-anaesthetic effects following specific treatments. The classification accuracy reaches up to 99%, presenting a semi-automated facial expression software that can assess mouse wellbeing [](doi:10.1371/journal.pone.0228059)

## Vision Transformer

Progression within the machine learning field has resulted in transformers, widely used within natural language processing (NLP). The transformer architecture uses attention mechanisms [](doi:10.48550/arXiv.1706.03762); while more traditional machine learning architectures like recurrent neural networks (RNNs)
process the input in a sequential manner, the transformer is able to simultaneously process the entire data sequence [](doi:10.48550/arXiv.1706.03762). This allows transformers to be trained on large data sets with
high computational efficiency [](doi:10.48550/arXiv.1706.03762).
The transformer architecture has been employed in computer vision tasks as well, resulting in the vision transformer (ViT) [](doi:10.48550/arXiv.2010.11929). The ViT has been applied to image classification
tasks, and beats state-of-the-art CNNs, reaching high accuracy on several image recognition
benchmarks, including ImageNet and CIFAR, when trained on large datasets, while requiring
significantly less computational resources [](doi:10.48550/arXiv.2010.11929).
The architecture for the ViT consists of a linear projection layer, transformer encoder, and multilayer perceptron (MLP) ({ref}`myFigure`A). The vision transformer, similarly to the NLP transformer,
breaks the input sequence (in this case a picture) into a grid of patches with fixed sizes, e.g. 16x16
pixels. Each patch, being a 2-dimensional array of pixel values, is flattened into a 1-dimensional vector,
so a 16x16 patch with 3 (RGB; Red, Green, Blue) colour channels is made up of 16*16*3 = 768 values.
Using a trainable linear layer, each of the resulting flattened patches are linearly projected into a fixeddimensional space, thus the 1-dimensional vector of 768 values will be projected into a new 1-
dimensional vector of e.g. 512 values. This serves the purpose of embedding the patches (now called
patch embeddings) into a space suitable for processing by a transformer encoder. To retain positional information from the original image, a positional embedding, corresponding to the original position of
the patch in the image, is added to each patch embedding. Prior to passing to the transformer encoder,
a learnable CLS token is added to the sequence of embedded patches. The state of the CLS token at the output of the transformer encoder acts as an image representation. The sequence of embeddings is passed to the transformer encoder, consisting of multiple layers, each comprising a multi-head selfattention (MSA) and a multi-layer perceptron (MLP) sublayer. Self-attention is a unique aspect to the transformer architecture and allows each of the patches in the image to attend to all other patches. A weighted sum of the patch embeddings, based on the similarity of query and key representations of the patches, is calculated, and the weights are derived using the dot product of the query and key pairs with a subsequent softmax operation. Multiple self-attention mechanisms, called heads, operate in parallel, each learning to pay attention to different elements of the image, and the output of all the attention heads are concatenated and linearly projected. The output of the MSA is passed to a feedforward neural network, the MLP. Before the MSA and MLP sublayers, layer normalization is applied, and skip connections exist around the MSA and MLP sublayers. Thus, at each encoder layer the MSA enable patches to interact globally, and the MLP processes these interactions, while the model builds a representation of the image through repeated processing through multiple layers. Finally, the representation, i.e. the CLS token, is sent to a classification (MLP) head, producing image classification [](doi:10.48550/arXiv.2010.11929)[](doi:10.48550/arXiv.1706.03762). Since the transformer models are based on attention mechanisms, it is possible to extract and visualize attention maps. Traditionally this is done using attention rollout, with the aim to visualize how the ViT distributes attention across image patches. Attention rollout averages attention weights across heads and multiply the weight matrices of all the layers recursively. For an example of visualized attention maps, see {ref}`myFigure`B,. Inspecting attention distributions yields more interpretable models [](doi:10.48550/arXiv.2005.00928)[](doi:10.48550/arXiv.2010.11929)[](doi:10.48550/arXiv.1706.03762).

```{figure} ./images/ViT_fig.png
:label: myFigure
:alt: Sunset at the beach
:align: center

A) Graphical depiction of a Vision Transformer. B) Example of visualized attention maps. From Dosovitskiy et al. (2021)
```
