# Logistic Regression and Classification

## Index

- What is Logistic Regression?
  - Classification
  - Logistic vs Linear
- How to slove?
  - Hypothesis Representation
  - Sigmoid/Logistic Function
  - Decision Boundary
  - Cost Function
  - Optimizer (Gradient Descent)
- Summary

<br/>

## 1. Classification

### Binary Classification

- 합격 / 불합격
- 생존 / 사망
- 개 / 고양이

### Multiclass Classification

- 개 / 고양이 / 말 / 사자 / 호랑이
- 붓꽃 분류: Iris setosa / Iris versicolor / Iris virginica

<br/>

## 2. Logistic vs Linear

| Logistic                                                     | Linear                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image](https://user-images.githubusercontent.com/64063767/117119643-53288f00-adcd-11eb-8384-d343a2c99046.png) | ![image](https://user-images.githubusercontent.com/64063767/117119675-60457e00-adcd-11eb-9307-482c88425a8b.png) |
| Discrete(Counted)                                            | Cotinius(Measured)                                           |
| shoe size                                                    | time, weight, height                                         |

```python
Logistic_Y = [[0], [0], [0], [1], [1], [1], [1]] # One Hot
Linear_Y = [828.67, 833.45, 819.23, 828.34, 831.65] # Numeric
```

<br/>

## 3. Hypothesis Representation

| ![image](https://user-images.githubusercontent.com/64063767/117120106-e4980100-adcd-11eb-9b7e-8a5495cebd28.png) | <img src="https://user-images.githubusercontent.com/64063767/117121028-0b0a6c00-adcf-11eb-82eb-ea210345755e.png" alt="image" style="zoom: 50%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

<br/>

## 4. Sigmoid(Logistic) Function

g(z) function out value is between 0 and 1
$$
Sigmoid: g(z) = 1 / (1+e^{-z})
$$
<br/>

## 5. Decision Boundary

| g(z) > 0.5                                                   | x1 + x2 = 3                                                  | x1^2 + x2^2 = 1                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image](https://user-images.githubusercontent.com/64063767/117129714-026b6300-adda-11eb-9c6d-f17c3c0295e6.png) | ![image](https://user-images.githubusercontent.com/64063767/117121474-9a178400-adcf-11eb-9d8b-6faa4ab4a845.png) | ![image](https://user-images.githubusercontent.com/64063767/117121504-a3085580-adcf-11eb-8526-b2ce6dc92fbc.png) |

<br/>

## 6. Cost Function

- How to minimize the cost?

<img src="https://user-images.githubusercontent.com/64063767/117122651-0e9ef280-add1-11eb-98eb-5f6823d24248.png" alt="image" style="zoom:50%;" />

- Not Convex -> Convex logistic regression cost function

<img src="https://user-images.githubusercontent.com/64063767/117123222-ba484280-add1-11eb-9936-3d85a9baa0f4.png" alt="image" style="zoom:50%;" />

<br/>

## 7. Optimization

- How to minimize the cost function?

| Cost function                                                | Optimization process                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://user-images.githubusercontent.com/64063767/117124083-d6001880-add2-11eb-922f-fc09a0023029.png" alt="image" style="zoom:50%;" /> | <img src="https://user-images.githubusercontent.com/64063767/117123914-9cc7a880-add2-11eb-9c2e-f21d54291bce.png" alt="image" style="zoom:50%;" /> |

