# Simple Linear Regression

## Regression

> **Regression**: **Regression toward the mean**_Sir Francis Galton

<br/>

## Linear Regression

데이터를 가장 잘 대변하는 직선의 방정식(기울기 a와 y절편 b)을 찾는 것
$$
y = ax + b
$$


<img src="https://user-images.githubusercontent.com/64063767/116804514-4a7c5280-ab5a-11eb-85fd-b15da0c139e1.png" alt="image" style="zoom:50%;" />

<br/>

| Hypothesis(가설)                                             | Cost(비용)                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| H(x) = Wx + b                                                | H(x) - y                                                     |
| <img src="https://user-images.githubusercontent.com/64063767/116804621-1b1a1580-ab5b-11eb-9670-8b5da01a841b.png" alt="image" style="zoom:50%;" /> | <img src="https://user-images.githubusercontent.com/64063767/116804649-57e60c80-ab5b-11eb-86b8-6227a26e0c1f.png" alt="image" style="zoom:50%;" /> |
|                                                              | MSE, RMSE etc.                                               |

<br/>

## Cost Function(비용 함수)

가설과 실제 데이터와의 차이를 Cost/Loss/Error라고 하고 이 **Cost 비용을 최소화**하는 직선을 찾음

- Cost function

  - W: weight(가중치)
  - b: bias

  $$
  cost(W, b) = (\Sigma_i^m(H(x_i) - y_i)^2) / m
  $$

- Goal: **Minimize Cost function**

