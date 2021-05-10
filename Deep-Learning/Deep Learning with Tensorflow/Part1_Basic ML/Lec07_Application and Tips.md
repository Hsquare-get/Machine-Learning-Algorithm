# Application and Tips

## 0. Index

- Learning rate
  - Gradient
  - Good and Bad Learning rate
  - Annealing the Learning rate (Decay)
- Data preprocessing
  - Standardization / Normalization
  - Noisy Data
- Overfitting
  - Regularization
  - L2 Norm

<br/>

## 1. Learning rate

**Learning rate** is a hyper-parameter that controls how much we are adjusting the weights with respect the loss gradient

<img src="https://user-images.githubusercontent.com/64063767/117673980-41d4ed80-b1e6-11eb-9fbf-a745f64c1682.png" alt="image" style="zoom: 67%;" />

### Good and Bad Learning rate

- High Learning Rate is **Overshooting**
- Normal Learning Rate is **0.01**
-  **3e-4** is the best learning rate for **Adam Optimizer**

<img src="https://user-images.githubusercontent.com/64063767/117675284-64b3d180-b1e7-11eb-81dd-19c8e264dda6.png" alt="image" style="zoom: 67%;" />

### Annealing the learning rate

학습하는 과정에서 Learning rate를 조절하는 기법을 **Learning rate Decay**라고 한다.

- Step decay
- Exponential decay
- 1/t decay

```python
def exponential_decay(epoch):
    initial_learning_rate = 0.01
    k = 0.96
    exp_learning_rate = initial_learning_rate * exp(-k*t)
    return exp_learning_rate

# Tensorflow Code
learning_rate = tf.train.exponential_decay(starter_learning_rate, global_step, 1000, 0.96, staircase=True)

# other decay methods
tf.train.exponential_decay
tf.train.inverse_time_decay
tf.train.natural_exp_decay
tf.train.piecewise_constant
tf.train.polynomial_decay
```