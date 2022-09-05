# Ch. 2 Probability

- 2 interpretations:
    - Frequentist- prob represent long run frequencies of events that can happen multiple times
    - Bayesian- prob represents our uncertainty about something (related to information content instead of repeated trials)
- 2 cases of uncertainty in predictions:
    - Epistemic (aka model)- ignorance of the data generation method/underlying causes
        - can be reduced by collecting more data
    - Aleatoric (aka data)- intrinsic variability
        - cannot be reduced by collecting more data
- low order summary stats can be insufficient
- inference- generalizing from sample data (usually also calculating degrees of certainty)
    - bayesian inference- represents degrees of certainty using probability theory
- bayes rule follows from the product rule of probability

## Ch. 4 Stats

### Bayesian Stats

- inference- modeling uncertainty about parameters using a prob distribution (as opposed to only a point estimate)
- posterior distribution $p(\theta | D)$ represents our uncertainty about the params givven the data
- prior distribution $p(\theta)$ reflects what we know before seeing the data
- likelihood function $p(D|\theta$ ) reflects the data we expect to see for each set of parameters


## Class Notes
- probabilistic approaches to ml has benefits
    - ml can be seen asreasoning under uncertainty (e.g. model outputs and params have uncertainty)
- regression, classification, generation, and discovery problems benefit from probabilistc formulations
- inference- computing the distribution that governs a model's parameters given data
    - major focus of the course
    - aka Bayesian ML
- empirical risk minimization is the standard approach to ml