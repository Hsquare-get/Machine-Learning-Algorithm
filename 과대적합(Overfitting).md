# 과대적합(Overfitting)

> 과대적합(Overfitting)이란 학습데이터에만 너무 잘 맞고, 검증데이터나 테스트데이터에는 잘 맞지 않는 현상을 과대적합이라고 한다.

- 복잡한 모형일수록, 데이터가 적을수록 과대적합(과적합)이 일어나기 쉬움
- 아래그림은 회귀분석에서 고차항을 넣었을때 만들어지는 직선

<img src="https://user-images.githubusercontent.com/64063767/109495755-08d81880-7ad3-11eb-8c49-97f7a479e00c.png" alt="image" style="zoom: 67%;" />

<br/>

### 분산(Variance)과 편파성(Bias)의 딜레마(Tradeoff)

![image](https://user-images.githubusercontent.com/64063767/109496155-9fa4d500-7ad3-11eb-9446-369e4a68b61c.png)

- 모형 f^(X)로 모집단의 전체 데이터를 예측할 때 발생하는 총 error를 계산하면 reducible error와 irreducible error로 표현되며, reducible error는 다시 분산과 편파성으로 구성된다.
- **분산** : 전체 데이터 집합 중 다른 학습데이터를 이용했을때, f^이 변하는 정도(**복잡한 모형일수록 분산이 높음**)
- **편파성** : 학습 알고리즘에서 잘못된 가정을 했을 때 발생하는 오차(**간단한 모형일수록 편파성이 높음**)
- 복잡한 모형 f^(X)을 사용하여 편파성을 줄이면, 반대로 분산이 커짐(간단한 모형일 경우엔 반대)
- 분산과 편파성이 적절하게 작은 모형을 찾는 것이 중요하다.

<img src="https://user-images.githubusercontent.com/64063767/109496872-9700ce80-7ad4-11eb-95b3-2d2b8630c8d3.png" alt="image" style="zoom: 67%;" />