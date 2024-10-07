# SHAP values

# Understanding of SHAP values and different epxlainers

I have looked at different explainers and what they are aimed at.
The [SHAP explainer](https://shap.readthedocs.io/en/latest/example_notebooks/image_examples/image_classification/Image%20Multi%20Class.html) sent I did not have success with so far. It seems to be a problem of the R50 I have adapted and trained does not fit the expected function of classification. 

I have instead found another SHAP explainer type called [Kernel](https://shap.github.io/shap/notebooks/ImageNet%20VGG16%20Model%20with%20Keras.html), which, based on the [GitHub README](https://github.com/shap/shap?tab=readme-ov-file), should be model agnostic, and thus more flexible, but also more computationally demanding. I have tried to adapt the code to fit my MSEloss model. The code is on [Git](https://github.com/AnnaStuckert/ViT_facemap/blob/AVS_development/ResNet50/kernelSHAP.ipynb).

How I think it works:

0) Train the model and load it, as well as a sample image

1) Segment the sample image using SK Learns SLIC. Currently sigma, compactness, and n_segments are kept the same as in the GitHub repo for the kernel shap explainer.

2) define masking function - what does it do?

3) define function where image is first masked, then preprocessed using preprocess_input () (I'm honestly not too sure what this function does, but I if try to apply the 'normal' preprocessing I do, it doesn't work, so I am sticking with this keras function for now. https://stackoverflow.com/questions/47555829/preprocess-input-method-in-keras - will have to develop on that and figure out what is going on.), and does a forward pass on the image.


Will add further description another day.

```{figure} ./images/SHAP_viz/SHAP visualization.png
:label: myFigure
:alt: SHAP
:align: center


```
