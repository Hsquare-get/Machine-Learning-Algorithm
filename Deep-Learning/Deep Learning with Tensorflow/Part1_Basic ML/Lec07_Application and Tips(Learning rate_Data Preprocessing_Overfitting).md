# Application and Tips

## 0. Index

- Learning rate
  - Gradient
  - Good and Bad Learning rate
  - Annealing the Learning rate (Decay)
- Data Preprocessing
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

<img src="https://user-images.githubusercontent.com/64063767/118359549-e8dad000-b5be-11eb-8959-0577ff90582a.png" alt="image" style="zoom:67%;" />

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

<br/>

## 2. Data Preprocessing

### Feature Scaling(data scaling)

- 모든 스케일링은 **테스트 데이터가 포함된 전체 데이터셋이 아닌 오로지 훈련 데이터에 대해서만 적용**되어야 한다.
- 이후 훈련 데이터와 테스트 데이터를 각각 스케일링한다.

- 일반적으로 목표변수(y) 데이터에 대한 스케일링은 진행하지 않는다.
- 모든 변수를 항상 같은 방식으로 스케일링할 필요는 없다. 변수의 특성에 따라 각기 다른 스케일링을 적용하는게 유리한 경우도 있다.

#### Normalization(정규화)

$$
x' = (x-x_{min}) / (x_{max} - x_{min})
$$

> **Min-Max 정규화**
>
> - 모든 feature에 대해 각각 0~1 범위 안의 값으로 변환하는 정규화 방법
> - 분류보다 회귀에 유용하다

```python
Normalization = (data - np.min(data, 0)) / (np.max(data, 0) - np.min(data, 0))
```

<br/>

#### Standardization(표준화)

$$
x' = (x-\mu) / \sigma
$$



> **Z-Score 표준화**
>
> - 데이터들의 정규분포를 평균이 0이고 분산이 1인 표준 정규 분포로 변환하는 방법
> - 이상치에 robust하다
> - 회귀보다 분류에 유용하다

```python
Standardization = (data - np.mean(data)) / sqrt(np.sum((data - np.mean(data)) ** 2) / np.count(data))
```

<br/>

### Noisy Data

<img src="https://user-images.githubusercontent.com/64063767/118359463-913c6480-b5be-11eb-84b7-d4ba332cec7f.png" alt="image" style="zoom:50%;" />

<br/>

## 3. Overfitting

![image](https://user-images.githubusercontent.com/64063767/118398827-3f1a4280-b695-11eb-867b-2a942ff0fcf6.png)

### Solution

#### (1) Set a features

- **Get more training data**: more data will actually make a difference (helps to fix high variance)

- **Smaller set of features**: dimensionality reduction(**PCA**) (fixes high variance)

  ```python
  from sklearn.decomposition import PCA
  pca = decomposition.PCA(n_components=3)
  pca.fit(X)
  X = pca.transform(X)

- **Add additional features**: hypothesis is too simple(underfit), make hypothesis more specific (fixes high bias)

<br/>

#### (2) Regularization (Add term to loss)

<img src="https://user-images.githubusercontent.com/64063767/118399786-c964a580-b699-11eb-8f94-61ef43242577.png" alt="image" style="zoom:67%;" />

```python
# Tensorflow code
L2_loss = tf.nn.l2_loss(w) # output = sum(t**2) / 2
```

