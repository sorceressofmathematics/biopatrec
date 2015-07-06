**NOTE: This is ongoing work and therefore the documentation found in this page is not 100% accurate until this notice has disappeared.**

This page gives a run down of the different control algorithms using an example with four simultaneous movements.

This was implemented and published in:

[Falk-Dahlin J., Evaluation of Post-Processing Strategies for Simultaneous Pattern Recognition Based Myoelectric Prosthetic Control, Master Thesis in Complex Adaptive Systems, Chalmers University of Technology, Sweden](http://publications.lib.chalmers.se/records/fulltext/178879/178879.pdf)

# Control Algorithms Example #

To better understand the different control algorithms that are available to choose from, an example using four simultaneous movements is presented here along with how the data is treated in each control algorithm.

In the following picture a patRec structure that is trained to recognize four simultaneous movements is presented. This structure contains, besides the information on how to make the classification, the following three fields, nOuts, mov and movOutIdx. These fields are used to set up the currently implemented control algorithms in one way or another.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/patRec.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/patRec.png)

When a prediction is made (this is done with the routine OneShotPatRecClassifier.m), a vector containing the predicted movement indices (outMov) is returned along with a vector containing the probabilities of all movements (outVec). These vectors are then used by the control algorithm (control is performed by the routine ApplyControl.m).

## Currently Implemented Control Algorithms ##
  * [MajorityVote](MajorityVote.md)
  * [MajorityVoteSimultaneous](MajorityVoteSimultaneous.md)
  * [BayesianFusion](BayesianFusion.md)
  * [Ramp](Ramp.md)
  * [RampModified](RampModified.md)
  * [CombinedControl](CombinedControl.md)

## MajorityVote ##

[MajorityVote](MajorityVote.md) control algorithm stores the predicted movements in an output buffer that has the same number of columns as nOuts. The predicted movement indices are used to set the columns of the predicted movements to 1 and 0 for the non predicted ones. The movements that are occuring most within the buffer are outputted.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/MajorityVote.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/MajorityVote.png)

Below is a simulation of real time pattern recognition of six simultaneous movements, both the predicted movements and the outputted movements are shown in the figure. Here a buffer size of 5 was used

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/simulationMajorityVote.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/simulationMajorityVote.png)

## MajorityVoteSimultaneous ##

[MajorityVoteSimultaneous](MajorityVoteSimultaneous.md) is a little different than the [MajorityVote](MajorityVote.md) control. This control algorithm stores the predicted movements in an output buffer that has the same number of columns as the size of the patRec movOutIdx list. This makes simultaneous movements, e.g. "Open Hand + Flex Hand" to have their own columns in the output buffer.

The problem that arise when [MajorityVote](MajorityVote.md) is used for simultaneous control is that if one degree of freedom is misclassified, e.g. "Open Hand + Flex Hand" is wanted but only "Flex Hand" is predicted, then "Open Hand" will occur fewer times in the output buffer than "Flex Hand" and thus only "Flex Hand" will be outputted until the buffer is emptied and refilled.

If the simultaneous movement get it's column in the output buffer this problem can be avoided.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/MajorityVoteSimultaneous.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/MajorityVoteSimultaneous.png)

Below is a simulation of real time pattern recognition of six simultaneous movements, both the predicted movements and the outputted movements are shown in the figure. Here a buffer size of 5 was used.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/simulation_MajorityVoteSimultaneous.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/simulation_MajorityVoteSimultaneous.png)

Compare the results with those for MajorityControl and one can see that the MajorityVoteSimultaneous does not have the movement interruptions that are present in MajorityVote.

## BayesianFusion ##

[BayesianFusion](BayesianFusion.md) operates on the outVec, i.e. the probabilities of the movements. The probabilities are stored in the output buffer and the product of each row is taken to give the probabilities of the output movements. To decrease the controller delay a weight matrix can be used to weigh the recent probabilities more then older ones. This weight matrix is turned on and off by setting the parameter "weights" to 1/0.

The weights also help with the fact that if the probability of a movement is 0 anywhere in the buffer, then the product of the probabilities also will be zero. By adding the weights rather then multiplying them, one makes sure that no probability in the buffer ever is zero.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/BayesianFusion.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/BayesianFusion.png)

## Ramp ##

The [Ramp](Ramp.md) strategy operates on the movement speeds rather than the output movements themselves. By limiting the initial speed of a movement, spurious misclassifications will not make as big impact on the outputted movement. The movement speed is increased with the number of consecutive predictions of a movement, but only the predicted movements are outputted.

The number of consecutive predictions are tracked with a counter, if a movement is predicted, the counter goes up, if not, the counter goes down by a number of countDown steps. By not setting the counter to zero directly when a movement is not predicted, the movement speed can be picked up fasted after spurious misclassifications.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/Ramp.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/Ramp.png)

The outputted movement speed for two different movements are shown in the figure below.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/speed_ramp.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/speed_ramp.png)

## RampModified ##

The [RampModified](RampModified.md) strategy handles the misclassifications differently than [Ramp](Ramp.md). Instead of using a downCounter parameter to decrease the counter it stores the counter vector into a buffer and uses the buffer to see how long ago the movement last was predicted. If the movement has been predicted within a certain number of predictions, the counter is resumed from the last value.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/RampModified.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/RampModified.png)

The outputted movement speed for two different movements are shown in the figure below.

![https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/speed_rampModified.png](https://biopatrec.googlecode.com/svn/wiki/img/controlAlgEx/speed_rampModified.png)

## CombinedControl ##

The [CombinedControl](CombinedControl.md) allows for the combination of two different control strategies where control algorithm one is first applied and then control algorithm two. This allow for smoothing of both the outputted movements and their speeds.