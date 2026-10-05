# Glossary

Plain-language definitions, grouped by topic. Each term is defined the way it's actually
used in this project.

## Programming (OOP)

| Term | Definition |
|---|---|
| **Class** | A blueprint describing what something has (data) and can do (behaviour). Nothing exists yet — it's just a design. |
| **Object / Instance** | One actual thing built from a class. Each object keeps its own separate copy of the data. |
| **Attribute** | A piece of data stored on an object (e.g. a model's weights). Persists for as long as the object exists. |
| **Method** | A function that belongs to a class, and can only be called through an object built from that class. |
| **Constructor (`__init__`)** | A special method that runs automatically, exactly once, the moment an object is created. Used to set up a model's initial structure and weights. |
| **`self`** | Refers to "the particular object this code is currently running for." Required whenever a method accesses another attribute or method belonging to the same object. |
| **Parameter** | A value passed into a method, used temporarily while that method runs, then discarded — not stored on the object unless explicitly saved with `self.`. |

## Data Structures

| Term | Definition |
|---|---|
| **Tensor / Array** | A container of numbers arranged along one or more dimensions. A single number is 0-dimensional, a list is 1D, a table is 2D, and so on. |
| **Shape** | How many values a tensor holds along each dimension, e.g. "100 samples by 17 features." |
| **Scalar, Vector, Matrix** | Names for tensors with 0, 1, and 2 dimensions respectively. |

## Network Structure

| Term | Definition |
|---|---|
| **Neuron / Perceptron** | A single computing unit: takes in several numbers, combines them with weights, adds a bias, and passes the result through an activation function. |
| **Input layer** | The raw features fed into the network — not an actual computing layer, just the entry point. |
| **Hidden layer** | A layer of neurons between the input and output, where intermediate features are learned. |
| **Output layer** | The final layer that produces the network's prediction. |
| **Weight** | A number representing the strength of the connection between two neurons. Learned during training. |
| **Bias** | An extra learnable number added to a neuron's weighted sum, letting it shift its output independent of the inputs. |
| **Parameters** | The collective term for all of a network's weights and biases — the values that get learned. |

## Forward Pass

| Term | Definition |
|---|---|
| **Pre-activation (`Z`)** | The weighted sum of a neuron's inputs, plus its bias — calculated *before* applying the activation function. |
| **Activation function** | A function applied to a neuron's pre-activation value, introducing non-linearity so the network can learn more than straight-line relationships. |
| **Activated output (`A`)** | The result after applying the activation function to `Z`. This is what gets passed to the next layer. |
| **Sigmoid** | An activation function that squashes any input into a value between 0 and 1. Commonly used for binary classification outputs, or (with care) hidden layers. |
| **ReLU (Rectified Linear Unit)** | An activation function that outputs the input directly if positive, otherwise outputs 0. The common modern default for hidden layers. |
| **Tanh** | An activation function similar in shape to sigmoid but squashing to (-1, 1) instead of (0, 1), centred at 0. |
| **Softmax** | An activation function used in multi-class classification output layers, converting raw scores into a probability distribution across all classes — values between 0 and 1 that sum to exactly 1. |
| **Logits** | The raw, pre-activation output values of a classification model's final layer, before being converted into probabilities (e.g. by softmax or sigmoid). |
| **Forward pass / Forward propagation** | The process of passing input data through the network, layer by layer, to produce a prediction. |

## Weight Initialization

| Term | Definition |
|---|---|
| **Weight initialization** | The process of assigning starting values to a network's weights before training begins. |
| **Symmetry breaking** | The reason weights are started as random, differing values rather than all identical (e.g. all zero) — so that different neurons can learn to detect different things, instead of all behaving identically forever. |
| **Seed (random seed)** | A fixed starting point for a random number generator, making its "random" output reproducible — the same sequence every time the code runs. |

## Task Type

| Term | Definition |
|---|---|
| **Regression** | Predicting a continuous numeric value (e.g. a severity score). Output layer typically has no activation function. |
| **Classification** | Predicting a category (e.g. disease vs. no disease). Output layer typically uses sigmoid (two categories) or softmax (more than two). |

## Loss and Optimization

| Term | Definition |
|---|---|
| **Loss function / Cost function** | A single number summarizing how wrong the network's predictions are, compared to the true values. |
| **Mean Squared Error (MSE)** | A loss function for regression: the average of the squared differences between predictions and true values. |
| **Cross-entropy** | A loss function for classification, measuring the difference between predicted probabilities and true class labels. |
| **Gradient** | A measure of how much the loss would change if a specific weight were adjusted slightly — tells you both direction and size of the needed update. |
| **Gradient descent** | The algorithm of repeatedly adjusting weights a small step in the direction that reduces the loss. |
| **Learning rate** | A small number controlling how large each gradient descent update step is. |
| **Chain rule** | The calculus rule that lets a complex derivative (loss with respect to an early-layer weight) be broken into a chain of simpler, local derivatives. |

## Backpropagation

| Term | Definition |
|---|---|
| **Backpropagation (backward propagation of errors)** | The algorithm that computes every weight's gradient by working backward from the output layer to the input layer, applying the chain rule layer by layer. |
| **Error signal / Delta** | An intermediate quantity computed at each layer during backpropagation, representing how much that layer contributed to the overall error. Reused to avoid recalculating gradients from scratch at every layer. |
| **Vanishing gradient problem** | A training failure where gradients become extremely small as they propagate backward (common with sigmoid, when neurons saturate near 0 or 1), causing earlier-layer weights to barely update, or not learn at all. |
| **Saturation** | When an activation function's output sits very close to its extreme values (e.g. sigmoid near 0 or 1), where its derivative is close to zero. |

## Data Handling

| Term | Definition |
|---|---|
| **Train/test split** | Dividing data into a portion used to train the model and a separate, held-out portion used to evaluate it on unseen examples. |
| **Data leakage** | When information that wouldn't be available in a real prediction scenario accidentally influences training or evaluation, making results look better than they truly are. |
| **Standardization** | Rescaling features to have mean 0 and standard deviation 1, so that no single feature dominates purely due to its numeric scale. |
| **Group-aware split** | A train/test split that keeps all records belonging to the same subject/group entirely on one side, preventing leakage through repeated measurements of the same subject. |

## Evaluation

| Term | Definition |
|---|---|
| **RMSE (Root Mean Squared Error)** | The square root of MSE — converts the loss back into the same units as the original target, making it directly interpretable. |
| **Baseline model** | The simplest possible comparison point (e.g. always predicting the average value), used to judge whether a model has learned anything genuinely useful. |
| **R² (R-squared)** | A score representing how much of the target's variance the model explains. 1 is perfect, 0 matches the baseline, negative is worse than the baseline. |
