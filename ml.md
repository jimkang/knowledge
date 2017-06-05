Machine learning
===

- Data and metrics are most important parts.

Things needed for ML to apply to a problem:

- A pattern exists
- We canot pin it down mathematically
- We have data on it

- Standard set-up finds the mapping from an input set to a *distribution* (probability space?) for the output set
- Finds best hypothesis rather than the true mapping.

Perceptron:
- Seeks a solution of wixi > threshold or wixi <= threshold
- Starts with a misclassified point. Updates the weight vector…accordingly?
- Estimate error pointwise.

- Training data is our sample we use to make inferences about the whole population.
  - Don't double-count the training data.
