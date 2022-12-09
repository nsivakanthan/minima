By: Nitharsan Sivakanthan

### Abstract:

Principal Component Analysis and K-means clustering can both be used to explore data and
uncover patterns. Here we look at several thousand COVID DNA sequences collected primarily
from Washington state. We uncover that there are certain locations and values on these
sequences that account for most of the variation in all the data and that there is potential to
differentiate these sequences into groups based on COVID variant or even origin. <!--more-->

### Background:

#### Principal Component Analysis (PCA)-

PCA is a dimensionality reduction technique that can be used to approximate data by creating
principal components that best describe the data.

PCA computes principal components 𝑍𝑛 using the following linear combination.

$$𝑍_𝑛 = 𝜙_{1𝑛}𝑥_{1} + 𝜙_{2𝑛}𝑥_{2} + ⋯ + 𝜙_{𝑝𝑛}𝑥_𝑃$$

Each 𝜙𝜌 is a linear combination of features p that correspond to the direction of greatest
variance and the observations x.

In performing PCA, our principal components now give the location of observations in a
reduced dimensional space with the principal components having a hierarchical order, the first
principal component being the direction of greatest variance.

Furthermore, a small number of principal components that account for much of the variance in
the data can be used to approximate the data.

#### Singular Value Decomposition (SVD)-

Another method for dimensionality reduction is SVD. When the data is scaled by mean and
variance, this method is equivalent to PCA. This method breaks down our observations into
three matrices: a matrix of the principal components, a matrix of the scaling of all principal
components called the singular values, and a matrix mapping the data to the principal
components.

Imputation of missing data can be performed using SVD to estimate the true values of the
missing data. First, the average is used to impute the missing data and then SVD is iteratively
used to obtain best estimates for the missing data.

#### K-means Clustering- 

This method clusters mainly numerical data into k groups of data that are closest together in
terms of Euclidian distance. Each of the k groups has a centroid and membership of each group
is determined by a points distance to each centroid. The centroids serve as a computationally
convenient way to minimize the distance between points within a group.

![Fig1](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig1.JPG 'Fig1')

Performing k-means clustering requires initialization of k random points for the initial centroids.
Then, we determine which groups points are allocated to based on their distance to these
centroids. New centroids are then computed based on the average of all the points in a group.
This process of allocating points to groups and computing new centroids is repeated until points
are no longer assigned to new centroids or equivalently when the centroids do not change.

### Methodology:

#### Data –

The data consists of genetic sequences of COVID mainly from Washington state collected from GISAID.
The sequences originally indicated the nucleobases that make up DNA denoted by the characters A, C,
G, and T. Our data has been processed to be numerical such that A = 1, C = 2, G = 3, and T = 4. There are
many values in the genetic sequences that are missing.

#### Process –

To perform PCA, the missing data must be dealt with. SVD imputation is used to estimate the true values
of the missing data. Once the imputation is complete, PCA is run on the imputed data. To further
explore the data, K-means is run on the imputed data to discover clusters of genetic sequences. Analysis
is performed on these results to find patterns and potential relationships.

### Results:

Once the data is prepped with the missing data imputed, PCA can be performed. Here are plots
of the proportion of variance explained by the data per principal component and a cumulative
sum plot, respectively.

![Fig2](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig2.JPG 'Fig2')

We will zoom in to get a better idea of the proportion of variance explained for the first 200
principal components.

![Fig3](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig3.JPG 'Fig3')

Below is a table of some numbers of principal components and their corresponding cumulative sum of
proportion of variance explained by the data:

![Fig4](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig4.JPG 'Fig4')

These plots and table indicate a significant portion of the variance can be explained by 20-50 principal
components, but for more accuracy a greater number of principal components can be considered.

Below is a table of the weights of the first 20 observations for the first three principal components:

![Fig5](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig5.JPG 'Fig5')

This table shows us that there are certain positions and values on these COVID genetic sequences that
could potentially indicate which variant of COVID the individual had or even help trace the origins of
their virus.

Next, k-means is used to cluster the data into groups. For the following analysis we will perform k-means
on the first 50 principal components, as this captures a large portion of the variance explained.
Conceptually here, it would make sense to cluster the data into groups based on the number of COVID
variants that are prevalent in Washington state. We will start with k = 4.

The following is a graph of the first two principal components and the four clusters resulting from kmeans each labeled by color:

![Fig6](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig6.JPG 'Fig6')

From only two principal components, it appears that the purple cluster does not seem to be much
different from the other clusters. However, if we also plot PC3, we get a better picture of the
differences.

![Fig7](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig7.JPG 'Fig7')

These are different orientations of the same plot of the first three principal components and the four
clusters resulting from k-means.

From these plots the differences between each cluster are more distinguishable, however it does appear
that maybe a different number of clusters could be used to differentiate some of the points farther
away.

Next, we will try k-means clustering with k = 5.

![Fig8](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig8.JPG 'Fig8')

Here, some of the observations that appeared as outliers before are now grouped together in their own
cluster. Again, it will be easier to distinguish these points when viewing the first three principal
components.

![Fig9](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig9.JPG 'Fig9')

Again, these are different orientations of the same plot of the first three principal components, but now
for five clusters resulting from k-means. Here it is easier to see the sequences that appear far away from
the other clusters are grouped together in their own cluster.

### Conclusion:

It appears that there are significant patterns between COVID genetic sequences from different
individuals in the Washington state area. When performing PCA, we observe certain positions
and values on the genetic sequences have a high influence on the variation of the sequences.
Clustering on many of the principal components from PCA, we can further distinguish
sequences potentially by their origin or variant of COVID.

### Appendix:

![Fig10](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig10.JPG 'Fig10')
![Fig11](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig11.JPG 'Fig11')
![Fig12](https://raw.githubusercontent.com/nsivakanthan/ML-Research-Papers/main/Figures-COVID-DNA-Sequences/fig12.JPG 'Fig12')

