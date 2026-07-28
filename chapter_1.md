# Chapter 1 - the machine learning landscape

Machine learning = science (and art) of programming computers to learn from data

## Best uses for ML models

Data mining = digging into data to discover hidden patterns

- Problems where existing solutions require lots of work
- Complex problems where traditional approaches don't give any good solutions
- Fluctuating environments
- Getting insights on complex problems and large datasets

## Types of learning

- Supervised = training set is labeled
- Unsupervised = training set is unlabeled
- Semi-supervised = training set is partially labeled
- Self-supervised = generating a fully labeled training set from a fully unlabeled one
- Reinforcement = an agent observes and interacts with environment, and using rewards/penalties, learns which policies earn the highest reward over time

## Batch vs online learning

Batch learning = can only be trained from scratch on the full dataset

- More susceptible to data drift/model decay
- Takes longer to train as the dataset expands

Online learning = can be trained in multiple batches

- Can set learning rate to determine how reactive the model is to new data points vs forgetting older ones
- Susceptible to performance drops if fed bad data over a period of time, difficult to resolve

## Instance-based vs model-based learning
