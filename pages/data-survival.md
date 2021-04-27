---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# Survival Analysis

## Data

- We consider an event (ie. death of a patient) and analyze the time to this event.
- The time to event must have a clear starting point.  This defines $t = 0$ and could be a heart attack or the first time an individual enters shelter.
- The end point of the timeline is when the event occurs.  The event could be death or a first interaction with police.  Sometimes the event is inevitable (ie. death) but often it is not (ie. disease re-diagnosis, interaction with police).
- Data is presented with length of time until event or exit from observation without event.


### Censoring and Truncation
- These concepts are best understood by considering calendar time rather than time to event.

- *Censoring*:
  + Measurement values are either known exactly or to have occurred in certain intervals.
  + These intervals are typically "before the start of the trial" and "after the end of the trial".

- *Truncation*:
  + We have no information at all about measurements that lie outside of a particular interval.


- *Right Censoring*:
  + A subject exits the trial without the event occuring and is considered a *survivor*.
  + The survivor's event time is *censored*.
  + The subject may have not been given enough time to develop the trait or the subject may never develop it (ie. a candidate never develops a particular disease, a baseball player never gets good enough to be in the top quartile of players).
  + All we know is that the subject has survived the trial.
  + *Generalized Type I sensoring* is when individuals enter the study at different times but the end of the study is pre-determined.  In this case, the start times of all individuals can be shifted to line up at $t=0$.


- *Left Censoring*:
  + We're aware the event has occurred for a subject before they're admitted to the study.
  + Event could have occurred before a calendar date or if a subject only comes under observation after the $t=0$ definition and after the event has occurred.  Example: A COVID study wants to track 8 year olds for 10 years to see when they develop the disease.  A 10 year old is admitted who already has the COVID antibodies but was asymptomatic so no infection time is known.

- *Left Truncation*:
  + We only observe individuals with timelines that exceed a certain cutoff point.
  + Individuals who experience the event prior to the cutoff are not observed (ie. common in true survival studies where death is the event).

- *Right Truncation*:
  + Individuals who experience an event after a cutoff time are not observed/included.
  + Example: A study that wants to focus on individuals that die of a disease.  Those individuals who die after the study concludes (the censored subjects) are excluded.


### Covariates
- Each individual is also presented with extra data (correlates/covariates) presented in summary style (no timestamped events).
- *Covariate*: Any variable that has a statistical relationship with a variable of interest.




## Functions

- *PDF/CDF*:
  - Characterize the random time to event, $T$, and are denoted $f(t)$ and $F(T)$.

- *Survivor Function*:
  - The probability that the event has not yet occured, $S(t) = P(T \geq t) = 1 - F(t)$.

- *Hazard Function*:
  - Almost equivalent to a PDF except that the probability is conditioned on $T \geq t$
$$
\begin{array}{rl}
h(t)
& = \lim_{\Delta \rightarrow 0} \frac{P(t \leq T < t+\Delta | T \geq t)}{\Delta} \\
& = \lim_{\Delta \rightarrow 0} \frac{P(t \leq T < t+\Delta \cap T \geq t)}{\Delta P(T\geq t)} \\
& = \lim_{\Delta \rightarrow 0} \frac{P(t \leq T < t+\Delta)}{\Delta P(T\geq t)} \\
& = \frac{f(t)}{S(t)}\\
& = -\frac{d}{dt}\ln S(t) \\
& = -\frac{1}{S(t)}\frac{d}{dt}S(t) \\
& = -\frac{1}{S(t)}\frac{d}{dt}[1-F(t)] \\
& = \frac{f(t)}{S(t)}\\
\end{array}
$$
  - Can be considered as the failure rate per year, given that the subject has survived until time $t$.  This captures the fact that the probability of failure will change as time passes (aging).

- *Cumulative Hazard Function*:
  - The integral of the hazard function $H(t) = \int_{0}^t h(u)du$.

- Due to the definitions of these functions, we have the relationship $S(t) = \exp[-H(t)]$ and $H(t) = -\log S(t)$.


## Survival Function Estimation

- Time is divided into intervals defined by the rank ordering of individuals in terms of study time.  Each of the transition points between intervals are *steps$.
- Since all individuals are alive at the start of the study, $S(0) = 1$.
- If $n_x$ and $d_x$ are the number alive and number who die at interval $x$, respectively, the probability of dying is $n_x/d_x$ and surviving is $(n_x-d_x)/n_x$.
- Right censored data will not cause a drop in the probability but it **does** result in a reduction in the population since they're no longer a member of the population at risk.
- Some general formulations only define steps at points where the survival function changes (presumably the population at risk is updated correctly, tho).
- The text uses the term "conditional" probability but it seems like we're taking the intersection of survival events here:

$$
\begin{array}{rl}
S(t) 
& = \prod_{k=0}^{\mbox{step}\leq t} P(\mbox{surviving interval $I_k$}) \\
& = \prod_{k=0}^{\mbox{step}\leq t} (n_k-d_k)/n_k
\end{array}
$$

- If the last survivor is right censored, $S(t)$ is undefined beyond that maximum time point instead of going to zero.

## Regression Models

- We want to estimate $h(t)$ which is strictly positive (it's a rate).  
- If we want to allow the parameters of the model to be unconstrained but still give us a positive rate, we can use $h(t) = \exp(\beta_0)$
- If we want to include covariate $x$ in our estimate of $h(t)$, we could use $h(t) = \exp(\beta_0 + \beta_1 x)$.  At this point, we have a hazard function that's constant with time.
- A fully parametric hazard function characterizes: 1)  the distribution of survival time (error component) and 2) how that distribution changes as a function of the covariates (system component).
- Sometimes we don't want to fully characterize the time distribution and just want to evaluate the relative impact of two different system components (ie. two different therapies).

- *Semiparameteric regression models*: Fully parametric structure but allow the dependence on time to remain unspecified.
- One formulation is $h(t,x,\beta) = h_0(t)r(x,\beta)$ where $h_0(t)$ is the *baseline hazard function*.
- If $H_0(t)$ is the cumulative function of $h_0(t)$, then the survival function is $S(t) = S_0(t)^{r(x,\beta)}$ where $S_0(t) = \exp[H_0(t)]$.
- If our covariate has a range of values (ie. age), we can associate $S_0(t)$ with the average age and the covariate $x$ = (age-average age) will scale $S_0(t)$ up when age is higher than the average and down when it's lower.

- *Hazard ratio*:
  - Compares two subjects with covariates $x_1$ and $x_0$.
  - Defined as ${\rm HR}(t,x_1,x_0) = r(x_1,\beta)/r(x_0,\beta)$.
  - HR is a constant and indicates the relative risk of the two subjects (ie. HR=2 means one group is "dying" at twice the rate of the other).

- *Cox proportional hazards model*:
  - Assumes $r(x,\beta) = \exp(x\beta)$ so that ${\rm HR}(t,x_1,x_0) = \exp[\beta(x_1-x_0)]$.


## Concodant Index

- Concordant means "in agreement" or "consistent".
- C-index equals the number of concordant pairs divided by the total number of possible evaluation pairs.
- A pair is concordant if the order of their predicted surival times is consistent with the actual data.
- Rather than actually predicting the time, individuals can be ordered based on their "risk scores", $r(x,\beta)$.
- These are determined directly from the Cox coefficients.

- C-index is equivalent to area under the ROC curve (AUC)
  - The AUC equals the probability the classifier ranks a randomly chosen positive index above a negative one.
  - Logistic regression computes a "score" for each instance equal to the probability that the instance is positive.
  - That score can be considered a random variable, $X$, that we apply a threshold, $T$, to.
  - If the instance is positive, it's score follows the conditional PDF $f(x\|{\rm pos}) = f_1(x)$.  If the instance is negative, it follows $f_0(x)$.
  - If we create a joint distribution, $P(X_1 > X_0)$ is the integral of the area above the unity slope line.
  - To find the AUC, we want to integrate over $T$ and for each value of $T$, we multiply the height of the curve (TPR) with the width of the horizontal steps (derivative of FPR). Subing in $f_0(x)$ for the derivative of FPR and the integral from threshold value $T'$ to $\infty$ for TPR gives the following

$$
\begin{array}{rl}
AUC
& = \int_\infty^\infty TPR(T)FPR'(T)dT \\
& = \int_\infty^\infty \int_\infty^\infty I(\alpha > T)f_1(\alpha)f_0(T)d\alpha dT \\
& = P(X_1 > X_0)
\end{array}
$$


- The sklearn ROC function just takes in binary labels indicating which cases are positive and scores (could be probability of positive, risk functions or whatever).  The function then sweeps up the threshold and creates the ROC curve.


## References
1. Hosmer, Lemeshow, May, "Applied Survival Analysis"
1. Guo, "Survival Analysis"
1. [Scikit: Understanding Predictions in Survival Analysis](https://scikit-survival.readthedocs.io/en/latest/user_guide/understanding_predictions.html)
1. [Introduction to Survival Analysis with scikit-survival](https://scikit-survival.readthedocs.io/en/latest/user_guide/00-introduction.html)



<br>
<br>
<br>
<br>
