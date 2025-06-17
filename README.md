# Do CNNs trained on globally discriminative patterns prefer to exploit absolute position

In 2020 Kayhan et al [1] showed that Convolutional layers are able to exploit absolute spatial
position to improve accuracy on the training set, often causing overfitting. However, the paper only
covers CNNs learning local features and neglects global pattern detection problems. While most 
common applications of convolutional layers regard local feature detection, global pattern 
recognition is highly relevant for problems such as scene recognition [2], tissue classification 
and segmentation [3], artistic style recognition [4] and art forgery detection [5]. Therefore, it
would be valuable to explore the degree to which the problem affects global pattern recognition.

My control dataset aims to provide a means of determining whether CNNs would exploit absolute
position when trained on global discriminative patterns, as opposed to local patterns.

I provide:
- A training set with positional bias
- A similar test set
- A dissimilar test set

The patterns that we want to distinguish between are:
- Class A, vertical sinusoidal waves (appearing as horizontal lines) of varying frequency and phase
- Class B, horizontal sinusoidal waves (appearing as vertical lines) of varying frequency and phase

The dataset is poisoned with white squares with class-bound position, such that:
- Training set: top-left for class A, bottom-right for class B
- Similar test set: top-left for class A, bottom-right for class B (same as the training set)
- Dissimilar test set: bottom-right for class A, top-left for class B (opposite of training set)

Training and similar test set class A example:

![alt text](https://github.com/LFWarsen/frmdl-control-dataset/blob/master/example_train_class_A.png "Training set class A example")

Training and similar test set class B example:

![alt text](https://github.com/LFWarsen/frmdl-control-dataset/blob/master/example_train_class_B.png "Training set class B example")

Dissimilar test set class A example:

![alt text](https://github.com/LFWarsen/frmdl-control-dataset/blob/master/example_dissimilar_test_class_A.png "Dissimilar test set class A example")

Dissimilar test set class B example:

![alt text](https://github.com/LFWarsen/frmdl-control-dataset/blob/master/example_dissimilar_test_class_B.png "Dissimilar test set class B example")

The goal is to measure the difference in performance of convolutional models between the test set containing the same positional bias as the training set and the test set containing the opposite
positional bias as the training set. This should reflect the degree to which the model over-relies on the positional bias in comparison to the actual translation-invariant global pattern. As per the
paper, the model performance should be evaluated for no-padding, zero same-padding, circular same-padding and zero full-padding.

This dataset is constructed to specifically evaluate whether convolutional neural networks rely on absolute spatial position when trained to recognize global discriminative patterns. The model is 
synthetic to limit the introduction of unintended features, which could result in accidental shortcut learning. The data should solely contain the desired global feature and the intentional 
positional bias feature. This way performance discrepancies can only be attributed to either of those features. A model that generalizes based on pattern orientation should perform similarly on 
both test sets, whereas one that exploits positional cues will show degraded performance on the dissimilar test set. This setup allows for a controlled and interpretable assessment of the 
network's sensitivity to absolute spatial bias in the context of global pattern recognition.

Dataset download url: https://drive.google.com/file/d/1XE4wSlPS1WlYu9O7N95EO2aTk9mJPVQo/view?usp=sharing

[1] O.S. Kayhan & J.C. van Gemert (2020): [On Translation Invariance in CNNs: Convolutional Layers can Exploit Absolute Spatial Location](https://arxiv.org/abs/2003.07064)

[2] B. Zhou, A. Lapedriza, A. Khosla, A. Oliva, & A. Torralba (2017): [Places: A 10 million Image Database for Scene Recognition](http://places.csail.mit.edu/)

[3] D.C. Cireşan, A. Giusti, L. M. Gambardella, & J. Schmidhuber (2012): [Deep Neural Networks Segment Neuronal Membranes in Electron Microscopy Images](https://papers.nips.cc/paper_files/paper/2012/hash/459a4ddcb586f24efd9395aa7662bc7c-Abstract.html)

[4] S. Karayev, A. Hertzmann, H. Winnemoeller, A. Agarwala, & T. Darrell (2014): [Recognizing Image Style](https://arxiv.org/abs/1311.3715)

[5] L. David, H. Pedrini, Z. Dias & A. Rocha (2021): [Connoisseur: Provenance Analysis in Paintings](https://doi.org/10.1109/SSCI50451.2021.9659547)
