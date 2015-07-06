# Introduction #

The BioPatRec allows you to create seemsly differet classifiers topologies using the available PatRec algorithms.

The topologies are created as part of OfflinePatRec, and later call in OneShotPatRecClassifier. Each topology uses a specific evaluation function named:

  * `PatRec_TopologyName`

All evaluation functions return two variables:

  * ''outMov'' is a vector with the predicted movements indices.

  * ''outVector'' is a vector with the classifier certanty of each movement, not only the predicted ones.

# Topologies #

## Single Classifier ##
(`PatRec_SingleClassifier`)

> A single classifier is created.

## Ago-antagonist ##
(`PatRec_AgoAntagonist`)

> This topology has as many classifiers as DoF (or Classes/2). Therefore it is assumed that consecutive classes are Ago-Antagonist movements organized in pairs per DoF. The classifier is trained only using the Ago-Antagonist data sets.

> The rest movements is considered as an exception. If this is present, the classifier considered the 2 movements of the DoF AND the rest movement (no movement) class.

> The output is given by the winner per DoF.

> NOTE: **Not good** for this application as it is! It will always predict as many movements as DoF. The following topology takes care of this issue.

## Ago-antagonist & Mixed ##
(`PatRec_AgoAntagonistRest`)

> Same than Ago-antagonist but the classifier is trained using the Ago-Antagonist sets, plus a mixed set containing the remaining classes. The rest movement (no movement) is also included in the training of each DoF if present.

> The output is given by the winner per DoF.


## One-vs-All ##
(`PatRec_OneVsAll`)

> This topology has as many classifiers as classes. A single classifier is trained to distinguish between a given class and the rest of the classes.

> The output of each classifier is assigned to the corresponding movement.

## One-vs-All Threshold ##
(`PatRec_OneVsAllT`)

> Same as One-vs-All but the output of each classifier is used to construct the vectorOut which is latter pass through a threshold selection.

## One-vs-One ##
(`PatRec_OneVsOne`)

> This topology has as `n*(n-1)/2` classifiers (n=classes).

> The output is normally given by major voting which makes it not suitable for simultaneous classification.

## One-vs-One DoF ##
(`PatRec_OneVsOneDoF`)

> Same than before but the losing movements in the DoF is made zero, and there is a threshold selection per class (one failure allowed).
> NOTE: Needs to be worked more, MO

# Auxilary routines #

The following routines are used by the topology functions to extract the data sets required for their topologies. This is all around the [xSets](xSets.md).

  * `ExtractSets_Stack`

> This function extract the corresponding set of selected movements (selSets). It keeps the format of [xSets](xSets.md) and xOuts but only with the rows corresponding to the selected movements with index in selSets

  * `ExtractSets_Stack_MixRest`

> It differs from `ExtractSets_Stack` by also including the remaining movements in a set with a single output labeled "mixed".

> NOTE: The number of sets in the mixed class and the selected movements (classe) would be normally different.


  * `ExtractSets_Stack_MixRestEqual`

> It differs from `ExtractSets_Stack_MixRest` by creating an equal number of sample between the selected sets and the mixed sets.

> NOTE: The number of sets per class would be the same.

## How to add a new Topology ##

The following must be done to add a "newTopology"

  * Add the name of the topology in the [GUI\_PatRec](GUI_PatRec.md) pop menu [pm\_SelectTopology](pm_SelectTopology.md), e.g. `newTopology`
  * Specify how this topology is created in OfflinePatRec
  * Make the case in OneShotPatRecClassifier
  * Create file `PatRec_newTopology` inside PatRec/Topologies where the output of this topology will be compute.