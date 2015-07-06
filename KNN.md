NOTE: This is an ongoing development and therefore the documentation is
not yet finalized.

# Introduction #

k-Nearest Neighbour Semi (k-NNS) is a modified algorithm of the traditional k-Nearest Neighbour (k-NN). It is a non-parametric lazy learning algorithm characterized as being one of the simplest machine learning algorithms. The purpose of k-NNS is focused on finding a group of k training patterns in the training set that are closest (in Euclidean distance) to the testing pattern followed by a certain classifications based upon the label on the predominance of particular classes in k.

The prediction of k-NNS differs from k-NN in that, the first has a prediction which is individual-class prediction based on proportion per class which exists in k, whereas the second is based on Majority Voting <sup>[1]</sup> to determine the dominant class in k.. More precisely, the output of k-NNS includes only the classes that gained a prediction more than or equal to 0.5, whereas the output of k-NN includes only one single winner, which is not suitable in the case of simultaneous movements prediction.

# Algorithm #

> The algorithm can be summarized by the following steps.
  1. Compute the Euclidean distance _d (p, x<sub>j</sub>)_ between test vector _p_ and the training set _x<sub>j</sub>_ for each _j=1,...,n_  where _n_ is the number of pattern in training sets.
  1. Find the _k-minimum_ distance _d<sub>k</sub>_ (group of the _k_ nearest vectors).
  1. Compute the proportion of each class in _k_.
  1. Inclusion each class that was gained a prediction more than or equal to 0.5 in the output of _k-NNS_.


# Implementation #

  * The training phase is performed for choosing the optimal _k_ (based on the lowest  Root Mean Square Error (_RMSE_)), by evaluating  the validation set with different values of _k_ (from _k_=1 to the number of windows per class(_nW_)).
  * Following the training phase, the validation set is added to the training set and used as references for making a prediction.


# Functions Roadmap #
> ## Training ##
The training procedure is only to choose optimal k.


  * `EvaluateKNN`
    * `InitKNN`
    * `FastTestKNN`
      * `K_NearestNeighbor`
        * `EuclidDist`
    * `FullTestKNN`
      * `K_NearestNeighbor`
        * `EuclidDist`
> ## Testing ##

  * `KNNTest`
    * `K_NearestNeighbor`
      * `EuclidDist`




---

# References: #
  1. Xindong Wu, Vipin Kumar,J. Ross Quinlan, Joydeep Ghosh, Qiang Yang, Hiroshi Motoda ,Geoffrey J. McLachlan, Angus Ng, Bing Liu, Philip S. Yu,Zhi-Hua Zhou, Michael Steinbach, David J. Hand and Dan Steinberg, ''Top 10 algorithms in data mining'', Springer-Verlag London Limited 2007,pp.(22-23).