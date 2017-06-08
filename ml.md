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

Markov assumption to reduce computational complexity:

P(D|A,B,C) ~= P(D|C)
(or ~= P(D|B,C) if you want to use two in the chain - 2-Markov assumption)

- Right of | is the condition.
- Left of | is what will happen
- P(D|A,B,C) means probabilty D will happen after you observe A then B then C.

P(Context|Word)

- To capture context, use something more dense than one-hot; high-dimensional vector of floats.
- Skip-Gram
  - Tries to predict how likely n terms are to appear before a term and how likely n terms are to appear after a term.
  - Uses nearest neighbors for this.
    - Dot product can be negative. So, take the exponent of it.
    - Then, normalize by dividing the above by the sum of all possible outcomes in that same context.
      - This is huge, unfortunately. Hence, there's some performance hack that takes care of that.
    - word2vec has **two** vectors for each word: Input vector and context vector.
      - Input word matrix, context word matrix.
 
Convolutions:

- Summarize a subset of 2D area multiple times?
- Subset of a locally-connected layer which is a subset of a dense layer
