By: Nitharsan Sivakanthan
    
Here I will go over how to make a multi-layer perceptron neural network from scratch. The derivation of the backpropagation algorithm will also be included. We will train the neural network on pictures of digits from sklearn's digit dataset to classify a picture into a digit. 

<!--more-->

### The Theory:

{% include youtube_embed.html id="eWUpS_s-q50&ab" %}  

#### Network Notation-

Neuron activations are denoted $$a_j^l$$, where the superscript $$l$$ is the layer and the subscript $$j$$ denotes the neuron index within that layer.

The first layer is the input data itself $$\mathbf{a}^1 = \mathbf{x}_i$$.

The hidden layer and output layer activities are written in terms of the weights $$w_{jk}^l$$, biases $$b_j^l$$, and the preceding layer activities $$a_k^{l-1}$$ as
$$a_j^l = \sigma(\sum_k w_{jk}^la_k^{l-1} + b_j^l)$$

The activation function $$\sigma(z)$$ is typically the ReLU or sigmoid function.

The input is simplified using the notation $$z_j^l = \sum_k w_{jk}^la_k^{l-1} + b_j^l$$ so that $$a_j^l = \sigma(z_j^l)$$

The weights and biases for the entire network are written with bold symbols $$\mathbf{w}, \mathbf{b}$$.

#### The Cost Function-

The data consists of $$n$$ pairs of observations for the input $$\mathbf{x}_i$$ and desired output layer response $$\mathbf{y}_i$$.

The goal is for the output layer $$\mathbf{a}^L(\mathbf{x}_i) = \begin{bmatrix} a_j^L(\mathbf{x}_i) \\ a_j^L(\mathbf{x}_i) \\ \vdots \\ a_j^L(\mathbf{x}_i) \end{bmatrix}$$ activities to match the desired output $$\mathbf{y}_i = \begin{bmatrix} y_{i1} \\ y_{i2} \\ \vdots \\ y_{iN_L} \end{bmatrix}$$


A cost $$C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})$$ describes the difference between the desired output $$\mathbf{y}_i$$ and the network's output for a given input $$\mathbf{x}_i$$. This cost is the sum of all cost values for each output neuron:

$$C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b}) = \sum_{j = 1}^{N_L}C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})$$

The cost might be a squared error or the cross-entropy loss.

The total cost over all input-output pairs $$C_{av}(\mathbf{w}, \mathbf{b})$$ is the average cost over the data.

$$C_{av}(\mathbf{w}, \mathbf{b}) = \frac{1}{n}\sum_{i = 1}^nC(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})$$

#### Gradient Descent-

We will use gradient descent to find the weights and biases $$\mathbf{w}, \mathbf{b}$$ that minimize the cost function.

The updates for the weights and biases are given by

$$w^l_{ij} \rightarrow w^l_{ij} - \alpha \frac{\partial C_{av}}{\partial w^l_{ij}}$$

$$b^l_{j} \rightarrow b^l_{j} - \alpha \frac{\partial C_{av}}{\partial b^l_{j}}$$

where $$\alpha > 0$$ is the learning rate.

So, we need to compute partial derivatives $$\displaystyle \frac{\partial C_{av}}{\partial w^l_{ij}}$$ and $$\displaystyle \frac{\partial C_{av}}{\partial b^l_{j}}$$.

Since 

$$C_{av}(\mathbf{w}, \mathbf{b}) = \frac{1}{n}\sum_{i = 1}^nC(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b}) = \frac{1}{n}\sum_{i = 1}^n\sum_{j = 1}^{N_L}C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})$$

we will start by computing derivatives $$\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial w^l_{ij}}$$ and $$\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial b^l_{j}}$$ and then we will sum the results over the output layer neurons and average over the training data.

To aid the computation of the derivatives, we will write the cost as a function of the last few layer's activities:

$$\begin{eqnarray}
C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b}) & = & \frac{1}{2}(y_{ij} - a_j^L(\mathbf{x}_i))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - a_j^L)^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(z_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^La_k^{L-1} + b_k^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(z_k^{L-1}) + b_k^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}a_l^{L-2} + b_l^{L-1}) + b_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}\sigma(z_l^{L-2}) + b_l^{L-1}) + b_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}\sigma(\sum_u w_{lu}^{L-2}a_u^{L-3} + b_u^{L-2}) + b_l^{L-1}) + b_j^L))^2 \nonumber 
\end{eqnarray}$$

Note that for simplicity, we drop the explicit reference to each activity being a function of the input $$\mathbf{x}_i$$.

Due to the activation function, this is a non-convex optimization problem. We will need to calculate gradients of each layer with respect to the weights and biases.

First, we compute partial derivatives for parameters in the output layer:

For this step, it will help to look at these parts of the Cost function while computing these partial derivatives.

$$\begin{eqnarray}
C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b}) & = & \frac{1}{2}(y_{ij} - a_j^L(\mathbf{x}_i))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - a_j^L)^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(z_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^La_k^{L-1} + b_j^L))^2 \nonumber \\
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial w_{jk}^L} & = & \frac{\partial C}{\partial a_{j}^L} \frac{\partial a_{j}^L}{\partial z_{j}^L} \frac{\partial z_{j}^L}{\partial w_{jk}^L}\nonumber \\
& = & (y_{ij} - a_j^L)(-\sigma\prime(z_j^L))(a_{k}^{L-1}) \nonumber \\
& = & (a_j^L - y_{ij})\sigma\prime(z_j^L)a_{k}^{L-1} \nonumber
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial b_{k}^L}& = & \frac{\partial C}{\partial a_{j}^L} \frac{\partial a_{j}^L}{\partial z_{j}^L} \frac{\partial z_{j}^L}{\partial b_{j}^L}\nonumber \\
& = & (y_{ij} - a_j^L)(-\sigma\prime(z_j^L))(1) \nonumber \\
& = & (a_j^L - y_{ij})\sigma\prime(z_j^L)\nonumber
\end{eqnarray}$$

We also need to compute partial derivatives for parameters in the second to last layer:

For this step, it will help to look at these parts of the Cost function while computing these partial derivatives.

$$\begin{eqnarray}
C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b}) & = & \frac{1}{2}(y_{ij} - a_j^L(\mathbf{x}_i))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - a_j^L)^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(z_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^La_k^{L-1} + b_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(z_k^{L-1}) + b_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}a_l^{L-2} + b_l^{L-1}) + b_j^L))^2 \nonumber \\ 
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial w_{kl}^{L-1}}& = & \frac{\partial C}{\partial a_{j}^L} \frac{\partial a_{j}^L}{\partial z_{j}^L} \frac{\partial z_{j}^L}{\partial a_{k}^{L-1}}\frac{\partial a_{k}^{L-1}}{\partial z_{k}^{L-1}} \frac{\partial z_{k}^{L-1}}{\partial w_{lu}^{L-1}}\nonumber \\
& = & (y_{ij} - a_j^L)(-\sigma\prime(z_j^L))(w_{jk}^{L}\sigma\prime(z_k^{L-1}))a_l^{L-2} \nonumber \\
& = & (a_j^L - y_{ij})\sigma\prime(z_j^L)w_{jk}^{L}\sigma\prime(z_k^{L-1})a_l^{L-2} \nonumber \\
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial b_{l}^{L-1}}& = & \frac{\partial C}{\partial a_{j}^L} \frac{\partial a_{j}^L}{\partial z_{j}^L} \frac{\partial z_{j}^L}{\partial a_{k}^{L-1}}\frac{\partial a_{k}^{L-1}}{\partial z_{k}^{L-1}} \frac{\partial z_{k}^{L-1}}{\partial b_{l}^{L-1}}\nonumber \\
& = & (y_{ij} - a_j^L)(-\sigma\prime(z_j^L))(w_{jk}^{L}\sigma\prime(z_k^{L-1})) \nonumber \\
& = & (a_j^L - y_{ij})\sigma\prime(z_j^L)w_{jk}^{L}\sigma\prime(z_k^{L-1}) \nonumber \\
\end{eqnarray}$$

Now, we compute partial derivatives for parameters in the third to last layer:

For this step, it will help to look at the Cost function including every layer while computing these partial derivatives.

$$\begin{eqnarray}
C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b}) & = & \frac{1}{2}(y_{ij} - a_j^L(\mathbf{x}_i))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - a_j^L)^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(z_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^La_k^{L-1} + b_k^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(z_k^{L-1}) + b_k^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}a_l^{L-2} + b_l^{L-1}) + b_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}\sigma(z_l^{L-2}) + b_l^{L-1}) + b_j^L))^2 \nonumber \\
& = & \frac{1}{2}(y_{ij} - \sigma(\sum_k w_{jk}^L\sigma(\sum_l w_{kl}^{L-1}\sigma(\sum_u w_{lu}^{L-2}a_u^{L-3} + b_u^{L-2}) + b_l^{L-1}) + b_j^L))^2 \nonumber 
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial w_{lu}^{L-2}}& = & \frac{\partial C}{\partial a_{j}^L} \frac{\partial a_{j}^L}{\partial z_{j}^L} \frac{\partial z_{j}^L}{\partial a_{k}^{L-1}}\frac{\partial a_{k}^{L-1}}{\partial z_{k}^{L-1}} \frac{\partial z_{k}^{L-1}}{\partial a_{l}^{L-2}}\frac{\partial a_{l}^{L-2}}{\partial z_{l}^{L-2}}\frac{\partial z_{l}^{L-2}}{\partial w_{lu}^{L-2}}\nonumber \\
& = & (y_{ij} - a_j^L)(-\sigma\prime(z_j^L))\sum_k(w_{jk}^{L}\sigma\prime(z_k^{L-1}))(w_{kl}^{L-1}\sigma\prime(z_l^{L-2}))a_u^{L-3} \nonumber \\
& = & (a_j^L - y_{ij})\sigma\prime(z_j^L)\sum_kw_{jk}^{L}\sigma\prime(z_k^{L-1})w_{kl}^{L-1}\sigma\prime(z_l^{L-2})a_u^{L-3} \nonumber \\
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})}{\partial b_{u}^{L-2}}& = & \frac{\partial C}{\partial a_{j}^L} \frac{\partial a_{j}^L}{\partial z_{j}^L} \frac{\partial z_{j}^L}{\partial a_{k}^{L-1}}\frac{\partial a_{k}^{L-1}}{\partial z_{k}^{L-1}} \frac{\partial z_{k}^{L-1}}{\partial a_{l}^{L-2}}\frac{\partial a_{l}^{L-2}}{\partial z_{l}^{L-2}}\frac{\partial z_{l}^{L-2}}{\partial b_{u}^{L-2}}\nonumber \\
& = & (y_{ij} - a_j^L)(-\sigma\prime(z_j^L))\sum_k(w_{jk}^{L}\sigma\prime(z_k^{L-1}))(w_{kl}^{L-1}\sigma\prime(z_l^{L-2}))(1) \nonumber \\
& = & (a_j^L - y_{ij})\sigma\prime(z_j^L)\sum_kw_{jk}^{L}\sigma\prime(z_k^{L-1})w_{kl}^{L-1}\sigma\prime(z_l^{L-2}) \nonumber \\
\end{eqnarray}$$

These are the partial derivatives of the Cost for the $$y_{ij}$$'s. We will now get the derivatives of the Cost for the $$y_{i}$$'s. Together these compose the gradient ($$\nabla$$) for each layer used for gradient descent.

To simplify the algorithm we will define $$\displaystyle \delta_j^l = \frac{\partial C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})}{\partial z_j^l}$$. 

Remember, 

$$C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b}) = \sum_{j = 1}^{N_L}C(\mathbf{x}_i, y_{ij}; \mathbf{w}, \mathbf{b})$$

We will use this to show that $$\displaystyle \frac{\partial C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})}{\partial w_{jk}^{l}}  = \delta_j^{l}a_k^{l-1}$$ where in the output layer $$\delta_j^L = (a_j^L - y_{ij}) \sigma'(z_j^L)$$ for a squared error loss and in other layers  $$\displaystyle \delta_m^{l} = \sum_{j = 1}^{N_{l+1}} \delta_j^{l+1} w_{jm}^{l+1} \sigma'(z_m^{l})$$.

First, we will show the result for the output layer:

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{i}; \mathbf{w}, \mathbf{b})}{\partial w_{mn}^L} & = & \frac{\partial}{\partial w_{mn}^L} C(y_i) \nonumber \\
& = & \sum_{j = 1}^{N_L} \frac{\partial}{\partial w_{mn}^L} C(y_{ij}) \nonumber \\
& = & \frac{\partial C(y_{im})}{\partial w_{mn}^L} \nonumber \\
& = & (a_j^L - y_{im})\sigma\prime(z_m^L)a_{n}^{L-1} \nonumber \\
& = & \delta_m^{L}a_n^{L-1}
\end{eqnarray}$$

Now, we will show the result holds for the two layers before the output layer:

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{i}; \mathbf{w}, \mathbf{b})}{\partial w_{mn}^{L-1}} & = & \frac{\partial}{\partial w_{mn}^{L-1}} C(y_i) \nonumber \\
& = & \sum_{j = 1}^{N_L} \frac{\partial}{\partial w_{mn}^{L-1}} C(y_{ij}) \nonumber \\
& = & \sum_{j = 1}^{N_L} (a_j^L - y_{ij})\sigma\prime(z_j^L)w_{jm}^L\sigma\prime(z_m^{L-1})a_{n}^{L-2} \nonumber \\
& = & \sum_{j = 1}^{N_L} \delta_j^Lw_{jm}^L\sigma\prime(z_m^{L-1})a_{n}^{L-2} \nonumber \\
& = & \delta_m^{L-1}a_n^{L-2}
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{i}; \mathbf{w}, \mathbf{b})}{\partial w_{mn}^{L-2}} & = & \frac{\partial}{\partial w_{mn}^{L-2}} C(y_i) \nonumber \\
& = & \sum_{j = 1}^{N_L} \frac{\partial}{\partial w_{mn}^{L-2}} C(y_{ij}) \nonumber \\
& = & \sum_{j = 1}^{N_L} (a_j^L - y_{ij})\sigma\prime(z_j^L)\sum_{k=1}^{N_{L-1}}w_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2})a_n^{L-3} \nonumber \\
& = & \sum_{j = 1}^{N_L} \delta_j^L\sum_{k=1}^{N_{L-1}}w_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2})a_n^{L-3} \nonumber \\
& = & \sum_{j = 1}^{N_L}\sum_{k=1}^{N_{L-1}}\delta_j^Lw_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2})a_n^{L-3} \nonumber \\
& = & \sum_{k=1}^{N_{L-1}}\sum_{j = 1}^{N_L}\delta_j^Lw_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2})a_n^{L-3} \nonumber \\
& = & \sum_{k=1}^{N_{L-1}}\delta_k^{L-1}w_{km}^{L-1}\sigma\prime(z_m^{L-2})a_n^{L-3} \nonumber \\
& = & \delta_m^{L-2}a_n^{L-3}
\end{eqnarray}$$

This pattern will repeat if we continue adding more layers. We have shown the result to be true. This result will help us signficantly when coding the backpropagation algorithm.

And similarly, we will show that $$\displaystyle \frac{\partial C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})}{\partial b_{j}^{l}}  = \delta_j^{l}$$ for all layers.

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})}{\partial b_{m}^{L}}& = & \frac{\partial}{\partial b_{m}^{L}} C(y_i) \nonumber \\
& = & \sum_{j = 1}^{N_L} \frac{\partial}{\partial b_{m}^L} C(y_{ij}) \nonumber \\
& = & \frac{\partial C(y_{im})}{\partial b_{m}^L} \nonumber \\
& = & (a_j^L - y_{im})\sigma\prime(z_m^L) \nonumber \\
& = & \delta_m^{L}
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{i}; \mathbf{w}, \mathbf{b})}{\partial b_{m}^{L-1}} & = & \frac{\partial}{\partial b_{m}^{L-1}} C(y_i) \nonumber \\
& = & \sum_{j = 1}^{N_L} \frac{\partial}{\partial b_{m}^{L-1}} C(y_{ij}) \nonumber \\
& = & \sum_{j = 1}^{N_L} (a_j^L - y_{ij})\sigma\prime(z_j^L)w_{jm}^L\sigma\prime(z_m^{L-1}) \nonumber \\
& = & \sum_{j = 1}^{N_L} \delta_j^Lw_{jm}^L\sigma\prime(z_m^{L-1}) \nonumber \\
& = & \delta_m^{L-1}
\end{eqnarray}$$

$$\begin{eqnarray}
\displaystyle \frac{\partial C(\mathbf{x}_i, y_{i}; \mathbf{w}, \mathbf{b})}{\partial b_{m}^{L-2}} & = & \frac{\partial}{\partial b_{m}^{L-2}} C(y_i) \nonumber \\
& = & \sum_{j = 1}^{N_L} \frac{\partial}{\partial b_{m}^{L-2}} C(y_{ij}) \nonumber \\
& = & \sum_{j = 1}^{N_L} (a_j^L - y_{ij})\sigma\prime(z_j^L)\sum_{k=1}^{N_{L-1}}w_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2}) \nonumber \\
& = & \sum_{j = 1}^{N_L} \delta_j^L\sum_{k=1}^{N_{L-1}}w_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2}) \nonumber \\
& = & \sum_{j = 1}^{N_L}\sum_{k=1}^{N_{L-1}}\delta_j^Lw_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2}) \nonumber \\
& = & \sum_{k=1}^{N_{L-1}}\sum_{j = 1}^{N_L}\delta_j^Lw_{jk}^{L}\sigma\prime(z_k^{L-1})w_{km}^{L-1}\sigma\prime(z_m^{L-2}) \nonumber \\
& = & \sum_{k=1}^{N_{L-1}}\delta_k^{L-1}w_{km}^{L-1}\sigma\prime(z_m^{L-2}) \nonumber \\
& = & \delta_m^{L-2}
\end{eqnarray}$$

Now, we have functions for the derivatives necessary to perform gradient descent.

Remember, the updates for the weights and biases are given by:

$$w^l_{ij} \rightarrow w^l_{ij} - \Delta w$$

$$b^l_{j} \rightarrow b^l_{j} - \Delta b$$

Once we have the gradients, we can calculate $$\Delta w$$ and $$\Delta b$$ by averaging together weights and biases over all of the training data:

$$\displaystyle\Delta w = -\alpha \nabla_w C_{av}(w,b) = -\alpha\frac{1}{n}\sum_{i=1}^n\nabla_w C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})$$

$$\displaystyle\Delta b = -\alpha \nabla_b C_{av}(w,b) = -\alpha\frac{1}{n}\sum_{i=1}^n\nabla_b C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})$$

#### Backpropagation-

To train the neural network, we use a method called backpropagation. The backpropagation algorithm consists of two parts, a forward pass and a backward pass. These are completed for each input-output pair from the training data with the goal of computing the gradients for the weights and biases for each layer of the network.

##### The Backward Pass

When, we computed the gradients for the weights and biases, there was a clear pattern.

For the output layer:

1.) Compute $$\delta_j^L$$ for both $$\nabla_w$$ and $$\nabla_b$$.

2.) For $$\nabla_w$$, we will also need the activations of the previous layer.

Next, when going backwards through the network (starting from the output, going towards the input), the next layer's gradients will consist of: 

1.) The previously calculated $$\delta$$ for $$\nabla_b$$

2.) The previously calculated $$\delta$$ and the next layer's activations for $$\nabla_w$$

This is the idea behind the backward pass of the backpropagation algorithm i.e. we have to start at the end of the network and propagate backwards through the network to calculate the gradients of the weights and biases.

##### The Forward Pass

To calculate our gradients, we will need to store the activations of every layer in the network. It is important to note, to reduce the number of computations when calculating the derivatives of the activation function, we will also want to store the $$z$$'s of every layer.

Furthermore, we must store these activations and $$z$$'s of every layer before doing the backward pass. This is where the forward pass comes from. We take our initialized or updated weights and biases and propagate them forward through the network to calculate and store the actiavtions and $$z$$'s. Then, we have what we need to perform the backward pass through the network to obtain the gradients of the weights and biases for each layer.

#### Stochastic Gradient Descent-

If we were to perform gradient descent on all of the training data at once, we would be computing an average of the changes in the weights and biases over all of the training data. Because we are updating the weights and biases after all of the gradients are calculated, this process can get computationally heavy and slow.

To speed up the process, we will use stochastic gradient descent. Instead of using all of the training data at once, we subset the training data into mini-batches. We still use all of the training data, but we update the weights and biases each time we go through a mini-batch.

In gradient descent, we iteratively take steps in the fastest direction possible to the optimal value. However, in this case, the fastest direction is computationally slow. In contrast, with stochastic gradient descent, we will take smaller steps, not always in the fastest direction toward the optimal value, but through iteration, gradient descent on these mini-batches will take us to an optimal value. These smaller steps are much faster computationally. Therefore, overall this process can be beneficial.

For stochastic gradient descent, we calculate $$\Delta w$$ and $$\Delta b$$ by averaging together weights and biases over all the mini-batches in a batch:

$$\displaystyle\Delta w = -\alpha \nabla_w C_{\text{mini-batch}}(w,b) = -\alpha\frac{1}{\text{batch size}}\sum_{i\in \text{mini-batch}}^{\text{batch size}}\nabla_w C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})$$

$$\displaystyle\Delta b = -\alpha \nabla_b C_{\text{mini-batch}}(w,b) = -\alpha\frac{1}{\text{batch size}}\sum_{i\in \text{mini-batch}}^{\text{batch size}}\nabla_b C(\mathbf{x}_i, \mathbf{y}_i; \mathbf{w}, \mathbf{b})$$

Now, we have everything we need to make our neural network from scratch!

### The Code:

We train a network to perform digit classification, using sklearn's digits data set. We will use a ReLU activation function, rather than the sigmoid activation function.

We will also use a squared error, as opposed to using the cross-entropy cost. The choice of the squared error is not ideal for this problem, but it simplifies some calculations and can be modified in the future.

To train and test the network, we will perform the following steps:

1.) Create the training and testing data

2.) Set the parameters of the model i.e. initialized layers, weights, betas, number of epochs, batch size, learning rate.

3.) Shuffle data and create mini-batches within an epoch.

4.) Compute gradients of weights and biases and use the gradients to update the weights and biases for each mini-batch.

5.) Test the updated weights and biases for each epoch and stop the training after the final epoch.

#### Python Libraries-


```python
# Import pandas, numpy, and matplotlib
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# seaborn is a data visualization library built on matplotlib
import seaborn as sns 
# set the plotting style 
sns.set_style("whitegrid")

# Train-test splits 
from sklearn.model_selection import train_test_split
from sklearn.utils import shuffle

# Model preprocessing
from sklearn import preprocessing

# Data
from sklearn import datasets

# Randomization for initializations
import random

# Model metrics
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay
```

#### Loading and Cleaning Data-


```python
digits = datasets.load_digits()

_, axes = plt.subplots(nrows=1, ncols=4, figsize=(10, 3))
for ax, image, label in zip(axes, digits.images, digits.target):
    ax.set_axis_off()
    ax.imshow(image, cmap=plt.cm.gray_r, interpolation="nearest")
    ax.set_title("Training: %i" % label)
```


    
![png](https://raw.githubusercontent.com/nsivakanthan/nsivakanthan.github.io/master/assets/output_48_0.png#center 'data')
    


Flatten the images to create the data set


```python
n_samples = len(digits.images)

data = digits.images.reshape((n_samples, -1))
```

Split the data into training and testing sets. Keep 20% of the data for the test set.


```python
X_train, X_test, y_train, y_test = train_test_split(data, digits.target, test_size=.2, shuffle=False)
```

Scale the predictor variables in the training set to have mean 0 and standard deviation 1.

Define the scaler using only the training data. For the validation set approach to work, we can not incorporate any knowledge of the validation set's properties into the model building process.


```python
scaler = preprocessing.StandardScaler().fit(X_train)
```

Perform the scaling transform on the predictors in the training and testing sets.


```python
X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

Transform the training labels into a 10-dimensional vector with a one in the position of the digit label and zeros elsewhere


```python
def vectorized_result(j):
    """Return a 10-dimensional unit vector with a 1.0 in the jth
    position and zeroes elsewhere.  This is used to convert a digit
    (0...9) into a corresponding desired output from the neural
    network."""
    e = np.zeros((10, 1))
    e[j] = 1.0
    return e
```


```python
Y_train = [vectorized_result(y) for y in y_train]
Y_test = [vectorized_result(y) for y in y_test]
```

#### Building the Neural Network-

These two functions apply the ReLU activation function and its derivative.


```python
# ReLU activation function
def relu(z):
  return np.where(z > 0, z, 0.0)

# Compute derivative of ReLU activation function
def reluprime(z):
  return np.where(z > 0, 1.0, 0.0)
```

This function initializes the weights and biases using a tuple of the sizes of each layer in the neural network. The weights and biases are created using a uniform random distribution. The values of these initializations may need changed to optimize different problems.


```python
# initialize biases and weights 
# sizes is a list containing number of neurons in each layer
# returns num_layers, biases and weights
def initialize(sizes):
  num_layers = len(sizes)
  biases = [np.random.uniform(low = 0,high = .1,size = (y, 1)) for y in sizes[1:]]
  weights = [np.random.uniform(low = 0, high = .1, size = (y, x)) for x, y in zip(sizes[:-1], sizes[1:])]
  return num_layers, biases, weights
```

The next two functions perform backpropagation. The following function computes the activations and $$z$$'s for each layer in the network using the most recent weights and biases. This is the forward pass through the network.


```python
# compute activations for each neuron; forward pass
# returns activations and z vectors for each layer
def forward(x, biases, weights):
  activation = x.reshape(-1,1)
  activations = [x.reshape(-1,1)] # list to store all the activations, layer by layer
  zs = [] # list to store all the z vectors, layer by layer
  for b, w in zip(biases, weights):
    z = w.dot(activation) + b
    zs.append(z)
    activation = relu(z)
    activations.append(activation)
  return activations, zs
```

This next function performs the backward pass through the network and returns the gradients for the weights and betas for a single input-output pair.


```python
# updates weight and biases for one input-output pair
def backward(y, activations, zs, num_layers, biases, weights):
  nabla_b = [np.zeros(b.shape) for b in biases]
  nabla_w = [np.zeros(w.shape) for w in weights]
  delta = (activations[-1] - y)*reluprime(zs[-1])  
  nabla_b[-1] = delta.reshape(-1,1)
  nabla_w[-1] = delta.reshape(-1,1).dot(activations[-2].reshape(-1,1).T)

  for l in range(2, num_layers):
    z = zs[-l]
    sp = reluprime(z)
    delta = np.dot(weights[-l+1].transpose(), delta) * sp
    nabla_b[-l] = delta
    nabla_w[-l] = delta.dot(activations[-l-1].T)
    return (nabla_b, nabla_w)
```

Here we perform gradient descent on the mini-batch. First, we sum together all the changes in weights and betas for each batch in the mini-batch. Then, these values are used in gradient descent to update the weights and biases.


```python
# perform gradient descent on a single mini-batch to update values
def descent_mini(mini_batch, learning_rate, num_layers, biases, weights):
  nabla_b = [np.zeros(b.shape) for b in biases]
  nabla_w = [np.zeros(w.shape) for w in weights]

  # Calculate changes in weights and biases for each input-output pair in the a mini-batch
  for x, y in mini_batch:
    activations, zs = forward(x, biases, weights)
    delta_nabla_b, delta_nabla_w = backward(y, activations, zs, num_layers, biases, weights)  
    nabla_b = [nb+dnb for nb, dnb in zip(nabla_b, delta_nabla_b)]
    nabla_w = [nw+dnw for nw, dnw in zip(nabla_w, delta_nabla_w)]

  # Perform gradient descent on the whole mini-batch using changes in weights and biases
  weights = [w-(learning_rate)*nw/len(mini_batch) for w, nw in zip(weights, nabla_w)]
  biases = [b-(learning_rate)*nb/len(mini_batch) for b, nb in zip(biases, nabla_b)]
  return weights, biases
```

This function will be used to evaluate the testing data. Each time this function is called, it uses the updated weights and biases to compute the final layer's activations, which will then be used to test the accuracy of the neural network.


```python
# generate activation digits from output layer
def network_output(a, biases, weights):
  for b, w in zip(biases, weights):
    a = relu(np.dot(w, a)+np.squeeze(b))
  return a
```

This function computes number of correct classifications over the testing data each time it is called.


```python
# evaluate performance of the network
def eval(test_data, biases, weights):
#   # must convert both y_train and y_test to vectorization for this code to work
#   test_results = [(np.argmax(network_output(x, biases, weights)), y)
#                    for (x, y) in test_data]
#   return sum(int(y[x]) for (x, y) in test_results)
  test_results = [((np.abs(network_output(x, biases, weights) - 1)).argmin(), y)
                    for (x, y) in test_data]
  return sum(int(x == y) for (x, y) in test_results)
```

Here is the main function. It will first group together the training and test data from the inputs 'X_train', 'y_train', 'X_test', 'Y_test'. Then, it will shuffle the training data to create mini-batches of size specified by the user input into the function. For each mini-batch, backpropagation and gradient descent will be performed and used to update the weights and biases for the next mini-batch. After all mini-batches are completed, those updated weights and biases are used to test the data. The output of this test is printed. This completes one epoch and the process is repeated for the number of epochs specified by the user input into the function. Once all epochs are complete, a confusion matrix is printed out using the final predictions on the testing data from the trained network.


```python
# perform stochastic gradient descent
def sgd(epochs, mini_batch_size, learning_rate, num_layers, biases, weights, X_train, y_train, X_test = None, y_test = None):
  training_data = list(zip(X_train, y_train))
  test_data = list(zip(X_test, y_test))
  
  if test_data: 
    n_test = len(test_data)
  n = len(training_data)

  for j in range(epochs):
    # create mini-batches
    random.shuffle(training_data)
    mini_batches = [training_data[k:k+mini_batch_size] for k in range(0, n, mini_batch_size)]

    # use gradient descent to calculate new weights and biases updating them after each mini-batch
    for mini_batch in mini_batches:
      weights, biases = descent_mini(mini_batch, learning_rate, num_layers, biases, weights)
    
    if test_data:
      print("Epoch {0}: {1}/{2}  accuracy = {3}".format(j, eval(test_data, biases, weights), n_test
                                                          , np.round(eval(test_data, biases, weights)/n_test, 4)))
    else:
      print("Epoch {0} complete".format(j))
  y_pred = np.asarray([(np.abs(network_output(x, biases, weights) - 1)).argmin() for x in X_test])
  cm = confusion_matrix(y_test, y_pred)
  cmd = ConfusionMatrixDisplay(cm)
  cmd.plot()
```

Here we initialize a network with three layers. The size of a single input is 64, therefore this is the size of the first layer. There are 10 digits that are possible outputs, therefore this is the size of the final layer. 

There are many factors involved with optimizing a neural network: the initialization of the sizes of the layers, the number of layers, the values of the initialized weights, the value of the initialized biases, the batch size, the learning rate, the train/test split. These values can be tweaked and experimented with to achieve the best results. There are methods of cross-validation and picking the best parameters, but I will not cover those here.


```python
# initialize size of NN
sizes = (64, 100, 10)

# initialize weights and biases; also returns number of layers
num_layers, biases, weights = initialize(sizes)

sgd(20, 10, .01, num_layers, biases, weights, X_train, Y_train, X_test, y_test)
```

    Epoch 0: 173/360  accuracy = 0.4806
    Epoch 1: 230/360  accuracy = 0.6389
    Epoch 2: 264/360  accuracy = 0.7333
    Epoch 3: 281/360  accuracy = 0.7806
    Epoch 4: 282/360  accuracy = 0.7833
    Epoch 5: 296/360  accuracy = 0.8222
    Epoch 6: 305/360  accuracy = 0.8472
    Epoch 7: 309/360  accuracy = 0.8583
    Epoch 8: 312/360  accuracy = 0.8667
    Epoch 9: 311/360  accuracy = 0.8639
    Epoch 10: 315/360  accuracy = 0.875
    Epoch 11: 316/360  accuracy = 0.8778
    Epoch 12: 316/360  accuracy = 0.8778
    Epoch 13: 317/360  accuracy = 0.8806
    Epoch 14: 318/360  accuracy = 0.8833
    Epoch 15: 317/360  accuracy = 0.8806
    Epoch 16: 318/360  accuracy = 0.8833
    Epoch 17: 318/360  accuracy = 0.8833
    Epoch 18: 318/360  accuracy = 0.8833
    Epoch 19: 320/360  accuracy = 0.8889
    


    
![png](https://raw.githubusercontent.com/nsivakanthan/nsivakanthan.github.io/master/assets/output_79_1.png#center 'Confusion Matrix')
    


Looking at the confusion matrix, it seems that the network is confusing many of the 1's with 9's. Many numbers are confused for 8's, 5's, and 1's. Some of these do not make much sense, for example 4's being confused for 8's. Overall, this network is performing well.

Finally, we have completed our neural network from scratch!

#### References:

1.) Coursework from DATA 5155 Numerical Methods at Seattle University taught by Associate Professor Brian Fischer, PhD.

2.) 3Blue1Brown videos on Neural Networks - https://www.3blue1brown.com/topics/neural-networks

3.) Code samples for "Neural Networks and Deep Learning" textbook - https://github.com/mnielsen/neural-networks-and-deep-learning
