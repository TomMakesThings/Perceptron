<div align="center">
  <h1>Perceptron for the Sum and Parity Problem</h1>
  <p><b>Code by <a href="https://github.com/TomMakesThings">TomMakesThings</a></b></p>
  <p><b><sub>December 2022</sub></b></p>
</div>

---

# About
Two variants of a perceptron are implemented from scratch in Python to classify 10 binary inputs (xᵢ = +/-1) according to whether:
<ol type="I">
  <li>Their sum Σxᵢ is positive or negative</li>
  <li>The parity of the inputs ∏xᵢ, i.e. the sign of their product, is positive or negative</li>
</ol>

<div align="center">
  <img width = 400 src="https://github.com/TomMakesThings/Perceptron/blob/assets/Images/Perceptron-Diagram.png">
</div>

## Network Initialisation
During initialistion, learning rate was specified as 0.01, the maximum number of epochs set as 100 and the activation function set as the step function.

$\text{step function: } f(x) = \text{0 if x < 0 else 1}$

The model's weights $i = 1, ..., N$ are randomly initialised by sampling from a normal distribution with mean $μ = 0$ and variance $σ = 1$. The bias unit's weight is set as zero.

$\text{if i} \neq \text{0, } w_{i} = \frac{1}{\sigma \sqrt{2\pi}}e ^ {-\frac{(x - \mu)^{2}}{2\sigma^{2}}}$

$\text{else } w_{i} = 0$

## Training, Testing and Validation Data
Training, testing and validation data is generated as an array of n random sequences with 10 binary digits, either -1 or 1. For the sum sign problem, the matching label for each sequence is inferred as 1 if the sum is positive and 0 if it is negative. For the product parity problem, 1 denotes the product sign is positive, while 0 is negative.

## Training
The perceptron is set to train until the max number of epochs is reached, or stops early if the training loss converges to 0. Within an epoch, data is randomly shuffled and the perceptron makes a prediction per sample. This prediction is derived from the raw output, i.e. the dot product of the weights and input vector values plus bias, passed through an activation function. Since the step activation function is set, predictions are 0 if the raw output is less than 0, and 1 otherwise. The difference between the predicted output and expected output is calculated and multiplied by the learning rate to determine the magnitude to update weights. For the bias unit, the weights are updated by directly adding this value, while for other nodes the weight update is multiplied by the sample's value. At the end of an epoch, training error is recorded via the mean squared error (MSE) loss function. The perceptron's performance is also evaluated on validation data and once training is complete, training and validation MSE are returned.

$\Delta w_{i} = \eta (y - p)$

$MSE = \frac{1}{n} \sum (y - p)^{2}$

## Testing
To evaluate training, MSE is plotted over time. For the sum sign problem, both training and validation loss converge quickly to 0 allowing training to be stopped early. The network generalises well as is able to be trained to achieve 100% accuracy on unseen test data. By contrast, the product parity problem, loss does not converge and fluctuation can be observed due to the per sample, stochastic nature of weight updates. Attempting to train over a larger number of epochs and tune learning rate does not help model convergence. This is because the parity problem, which is a generalisation of the XOR problem, is not linearly separable. Therefore, unlike the sum problem, it is not solvable using a single-layer perceptron requires a multi-layer perceptron.

<div align="center">
  <img width = 700 src="https://github.com/TomMakesThings/Perceptron/blob/assets/Images/Training-Results.png">
</div>
