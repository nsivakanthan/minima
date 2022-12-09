![Banner](https://raw.githubusercontent.com/nsivakanthan/nsivakanthan.github.io/master/images/neural-network.JPG 'Banner')

By: Nitharsan Sivakanthan

### Abstract:

Convolution Neural Networks have been used frequently to classify images into categories.
Using this deep learning algorithm paired with computational power, models have been trained
on different datasets capable of achieving amazing results in classification. We train a model to
classify images of birds into one of 18 species common to the western Washington State area. <!--more-->
After tuning for parameters, the best model was able to achieve accuracy on the testing data of
roughly 50%. With more computational power, we expect to be able to reach higher accuracy.

### Problem Statement:

We want to classify images of birds common in western Washington State by their species.

### Background:

#### Neural Networks –

Neural networks take on an input layer, apply hidden layers to this input layer, and obtain an
output layer. These hidden layers allow us to perform various linear and nonlinear
transformations to each layer’s input ultimately providing us with an output. The more inputs in
our input layer and the more hidden layers we filter through, the more complex the neural
network gets.

![Fig1](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig1.JPG 'Fig1')

Each layer consists of nodes that establish linear connections between nodes of other layer(s). The hidden layers have nonlinear activation functions that compute the linear transformations used to connect nodes between layers. There are various activation functions that are convenient to use in these hidden layers because of their computational ease, particularly regarding their differentiability. 

#### Convolution Neural Networks (CNN) –

![Fig2](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig2.JPG 'Fig2')

Convolution Neural Networks are useful for image classification problems. These networks use
a convolution layer to discover patterns or features in the image inputs. For each image, the
algorithm will compare groups of pixels of that image and compute a filtered value. These
filtered values are then generalized into a pooling layer which creates a new general image of
the feature found in the convolution layer. The algorithm can repeat this process multiple
times. We can use these connects made between images and features to predict what is in a
new image based on the images used to train the algorithm.

#### Model Parameters -

Neural network algorithms have many parameters: number of units, activation function, input
shape, dropout rate, number of epochs, batch size, and validation split. In addition, for
convolution neural networks, we must provide the algorithm with a kernel size, pool size, and
number of filters.

Below is a table with a description of each of these parameters.

![Fig3](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig3.JPG 'Fig3')

### Methodology:

#### Data –

The images were sourced from the Birds 400 dataset on Kaggle. The dataset consists of over 60,000 images across 400 species. For this paper, we use up to 60 images for each of 18 species of birds common to the western Washington State area. All the images are 224 x 224 x 3 dimensions, in color, and in the jpg format. 

#### Process – 

After preparing the data for the CNN, we first process the algorithm on a subset of our data to make sure the CNN is working properly. Once this model is complete, we train a model now utilizing all the data to establish a baseline model. We train more models tuning for parameters and compare the testing accuracy with the baseline model to choose the best model. 

### Results:

For each of our trained models, there are three convolution and pooling layers in this model. Each pair of convolution and pooling layer is accompanied by a layer dropout. The input shape is the same for each model. Relu and softmax activation functions are used for all the models. And the categorical cross-entropy is used to calculate loss. 

#### Model with subset of data-

Using only 10 images of each of the 18 species of birds in the training data, a CNN model is trained to ensure the algorithm works properly on the data.

This model achieves 33% accuracy on the testing data.

#### Baseline model-

Now our models will use 30 images for the training data and 30 images for the testing data for sake of computational ease. The pseudocode provided in the Appendix is for the baseline model. All the parameters chosen for this baseline model can be found there.

This model achieves 49.44% accuracy on the testing data.

#### Parameter Tuning-

Next, we train models that change certain parameters to see its effect on the testing accuracy compared to the testing accuracy of the baseline model. The table below summarizes this process.

![Fig4](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig4.JPG 'Fig4')

The parameters chosen in the baseline model seem to be close to optimal. With more Epochs we can slightly increase the accuracy of the model on the testing data. 

### Conclusion:

Using deep learning, we developed a model that can classify an image of a bird into one of 18 species of birds common to western Washington State area with roughly 50% accuracy. There is potential to increase the level of accuracy of the model with more computational power and better tuning. 

### Appendix:

![Fig5](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig5.JPG 'Fig5')
![Fig6](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig6.JPG 'Fig6')
![Fig7](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-Image-Classification-Birds/fig7.JPG 'Fig7')
