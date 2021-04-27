---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# Evaluating Classification Performance

- For the following, assume a $K=2$ binary classifier.
- The training set contains some set of positive cases, $P$, and negative cases, $N$ so that the total number of training examples in our set is $M = \\|P\\| + \\|M\\|$.
- $\|P\|$ and $\|N\|$ are condition positive and condition negative, respectively.
- Prevalence: Condition positive divided by total population.
- The classifier is attempting to identify the positive cases and its operation is denoted by the $\hat{\cdot}$ symbol.
- After applying the classifier to the training set, we have the following four sets:
  1. True positives, $\hat{P}$.
  1. False positives, $\hat{N}$.
  1. True negatives, $\bar{N} = N - \hat{N}$.
  1. False negatives, $\bar{P} = P - \hat{P}$.
- It helps to think of the hat indicating elements the test thinks are positive and the bar indicating elements that the test thinks are negative.

## Confusion Matrix
- If we have $K$ classes, the confusion matrix is $K \times K$.  The row and column indices correspond to the class indicies and element $ij$ is the number of times a datapoint from class $i$ is identified by the algorithm as class $j$.  A perfect predictor has a diagonal confusion matrix.
- If $K=2$, the confusion matrix elements are:

$$
\left[
\begin{array}{cc}
|\hat{P}| & |\hat{N}| \\
|\bar{P}| & |\bar{N}|
\end{array}
\right]
$$

## Metrics

- For this discussion, a *conservative test* is one that classifies as positive only when it is very sure (very few false positives).  A *sloppy test* is one that is very quick to classify positive cases (lots of false positives).

- Metrics that quantify how positive cases are classified (sum to 1):

  - **True Positive Rate (Sensitivity/Hit Rate/Recall):**
    - $\|\hat{P}\|/\|P\| \simeq P(\mbox{positive classification}\|\mbox{positive sample})$
    - Evaluates how good we are at spotting positive cases.
    - A conservative test would have low sensitivity but a very sloppy test that indicates a positive result for all samples would have a sensitivity of 1.

  - **False Negative Rate (Miss Rate/Type II Error):**
    - $\|\bar{P}\|/\|P\| \simeq P(\mbox{negative classification}\|\mbox{positive sample})$
    - A conservative test would have a high false negative rate and a sloppy test would have a low one.

  - These two metrics tend to reward the same kind of test (conservative does poorly and sloppy does well).  This is likely why most people only talk about sensitivity.
  

- Metrics that quantify how negative cases are classified (sum to 1):

  - **False Positive Rate (False Alarm Rate/Fall-Out/Type I Error):**
    - $\|\hat{N}\|/\|N\| \simeq P(\mbox{positive classification}\|\mbox{negative sample})$
    - Indicates the proportion of negative samples that are classified as positive.
    - Conservative tests do well here because they only classify as positive if they're very sure.  A sloppy test will score poorly here since it lumps in a bunch of negative cases with it's positive classifications.

  - **True Negative Rate (Specificity):**
    - $\|\bar{N}\|/\|N\| = (\|N\|-\|\hat{N}\|)/\|N\| \simeq P(\mbox{negative classification}\|\mbox{negative sample})$
    - Conservative tests do well here since they mistake very few negative cases for positive.  Sloppy tests do poorly.

  - Both of these metrics reward a conservative test.

- The classic tradeoff made by ROC curves is true positive rate (sensitivity) versus false positive rate (false alarm rate) to strike the right balance between conservative and sloppy testing.

- There are a variety of other metrics that attempt to quantify overall test performance:

  - **Accuracy:**
    - $(\|\hat{P}\|+\|\bar{N}\|)/(\|N\|+\|P\|) \simeq P(\mbox{correct classification})$
    - Rewards *both* sensitivity (large $\hat{P}$) and specificity (small $\hat{N}$ or large $\bar{N}$).
    - Usually a poor metric for rare events since a very insensitive test can still achieve a high level of accuracy if $\bar{N}$ is very high.

  - **Confidence/Precision/Positive Predicted Value:**
    - $\|\hat{P}\|/(\|\hat{P}+\hat{N}\|) \simeq P(\mbox{positive sample}\|\mbox{positive classification})$
    - A conservative test with a large number of false negatives could have very high confidence.

  - **False Discovery Rate:**
    - $\|\hat{N}\|/(\|\hat{P}+\hat{N}\|) \simeq P(\mbox{negative sample}\|\mbox{positive classification})$

  - **False Omission Rate:**
    - $\|\bar{P}\|/(\|\bar{P}+\bar{N}\|) \simeq P(\mbox{positive sample}\|\mbox{negative classification})$
  
  - **False Omission Rate:**
    - $\|\bar{N}\|/(\|\bar{P}+\bar{N}\|) \simeq P(\mbox{negative sample}\|\mbox{negative classification})$



- Detecting chronic shelter use:
  - Accuracy is a poor metric since only 3% (clustering) or 4.8% (DI definition) of DI clients are chronic.
  - Confidence is important.  If a test indicates a client is chronic, we want to make sure that they actually are.
  - Sensitivity is also important since we want to ensure we're catching everyone who needs help.
  - We can use false discovery rate to estimate how many folks are getting help who may not need it.  

 
## Receiver Operating Characteristic (ROC) Curves

- An ROC curve plots true positive rate (sensitivity) versus false positive rate (false alarm rate).
- True positive rate rewards a sloppy test and false positive rate rewards a conservative test.
- Any binary classifier can be represented as a single point on the curve but often classifiers that use a threshold are represented as curves that are generated by sweeping the threshold over all possible values.

- For a very low threshold, all values are classified as positive so true positive rate is 1 (all positives are classified as positive) and false alarm rate is 1 (all negatives are classified as positive).
- For a very high threshold, all values are classified as negative so the true positive rate is 0 (no positives are classified as positive) and false alarm rate is 0 (no negatives are classified as positive).
- The worst possible performance is the straight line on the ROC curve where sensitivity equals false alarm rate.

- Example:
  - Consider a case with 100 cases where $\|P\|$ = 10 and $\|N\|$ = 90.
  - A coin toss test:
    + $\hat{P}$ = 5, $\hat{N}$ = 45, $\bar{P}$ = 5 and $\bar{N}$ = 45
    + Sensitivity: $\|\hat{P}\|/\|P\|$ = 5/10 = 0.5
    + False Alarm Rate: $\|\hat{N}\|/\|N\|$ = 45/90 = 0.5
  - The other points on the slope 1 line would be achieved by tests that randomly assign positive tests with a different probability (ie. a random test that classifies 20\% cases as positive would have a sensitivity and false alarm rate of 0.2).
  - An improved test:
    + $\hat{P}$ = 8, $\hat{N}$ = 9, $\bar{P}$ = 2 and $\bar{N}$ = 81
    + Sensitivity: $\|\hat{P}\|/\|P\|$ = 8/10 = 0.8
    + False Alarm Rate: $\|\hat{N}\|/\|N\|$ = 9/90 = 0.1
    + Much closer to the upper left corner.


## References
1. [Wikipedia's ROC Discussion.](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)
1. Furnkranz, Gamberger, Lavrac, "Foundations of Rule Learning", Springer.
