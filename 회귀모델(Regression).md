# 회귀(Regression)

## 0. 회귀분석 가정

회귀분석에 앞서 전제되는 네가지 가정들을 충족해야한다.

1. **선형성**: 종속변수와 독립변수는 선형적인 관계를 가져야 한다.
2. **독립성**: 다중회귀에서 독립변수들 간에 서로 독립적이어야 한다.
3. **잔차의 등분산성**: 잔차가 특정한 패턴 없이 고르게 분포되어있어야 한다.
4. **잔차의 정규성**: 잔차들의 분포가 정규 분포를 이루어야 한다. (표본이 크다면 잔차의 정규성 가정은 생략될 수 있다)

<br/>

## 1. 선형 회귀(Linear Regression)

> **회귀 계수(weight)를 선형 결합으로 표현할 수 있는 모델**
>
> 아래 두 모델식 모두 선형 회귀 모델로 표현 가능

![image](https://user-images.githubusercontent.com/64063767/152646139-84490b54-e7a4-4aeb-9c5a-f4576ab82c55.png)

![image](https://user-images.githubusercontent.com/64063767/152646015-578016b7-760e-4eed-a711-164eea76e528.png)

<br/>

### 1.1 단순선형 회귀(Simple Linear Regression)

> 독립변수가 1개인 회귀 모델

![simple linear eq](https://user-images.githubusercontent.com/64063767/152642504-2f78d802-eae8-4e81-9add-b8f6e102dacd.png)

![image](https://user-images.githubusercontent.com/64063767/152644436-d7b5b607-c32b-4100-832e-b282fb7aaafd.png)

### 1.2 다중선형 회귀(Multiple Linear Regression)

> 독립변수가 2개 이상인 회귀 모델

![multiple linear eq1](https://user-images.githubusercontent.com/64063767/152643045-47cd029b-8854-4f92-af8f-5bdd22655223.png)

![multiple linear eq2](https://user-images.githubusercontent.com/64063767/152643046-fdf5410d-6603-40eb-8032-8d0c7aaceb68.png)

![image](https://user-images.githubusercontent.com/64063767/152644491-166d1a9f-e32c-4ab7-b0d5-feb569dfc860.png)

### 1.3 다항 회귀(Polynomial Regression)

> 모델 항이 제곱근, 2차항, 3차항, 변수결합항 등으로 다양하게 구성된 회귀 모델
>
> **다항 회귀는 선형회귀**이다.
>
> 고차항이 추가될수록 과대적합(Overfitting)이 일어날 가능성이 매우 높다. (Low Bias - High Variance)

![polynomial eq](https://user-images.githubusercontent.com/64063767/152643051-b1b60569-ae63-48d3-bde7-0c367e78dba4.png)

![image](https://user-images.githubusercontent.com/64063767/152645619-1aa42756-447f-4edb-bcec-b5cca03fa10e.png)

<br/>

## 2. 비선형 회귀(Non-Linear Regression)

> 회귀에서 선형 회귀와 비선형 회귀를 나누는 기준은 **회귀계수(weight)가 선형적으로 결합됐는지 아닌지로 구분**한다.
>
> **독립변수의 선형성과는 무관**하다.

![non_linear eq1](https://user-images.githubusercontent.com/64063767/152643048-b21cdfa8-f1cb-4bd1-badf-b1f16e0925c5.png)

![non_linear eq2](https://user-images.githubusercontent.com/64063767/152646325-e924795a-ddb0-4b89-b39e-a4791a340022.png)

<br/>

## 3. 규제(Regularization)

![minimize cost](https://user-images.githubusercontent.com/64063767/152643822-48af44e7-1b00-45b1-9d83-b07e42a1682a.png)

- 회귀 모델이 적절히 데이터에 적합하면서도 회귀 계수가 기하급수적으로 커지는 것을 제어하는 방법
- 규제 방법은 비용함수에 alpha 값으로 페널티를 부여해 **회귀 계수 값의 크기를 감소**시켜 **과적합(Overfitting)을 개선하기 위해 사용**한다.

- **최적 모델을 위한 Cost 함수 구성요소 = 학습데이터 잔차오류 최소화 + 회귀계수 크기 제어**
- alpha는 학습 데이터 적합 정도와 회귀 계수 값의 크기 제어를 수행하는 튜닝 파라미터
  - alpha 감소 -> Cost 최소화가 목표
  - alpha 증가 -> 회귀 계수 W 감소를 목표

### 3.1 L2 Regularization

- **W의 제곱**에 대해 페널티를 부여하는 규제 방식
- L2 규제를 적용한 선형 회귀를 **릿지(Ridge) 회귀 모델**이라 한다.
- L2 규제를 통해 회귀 계수의 크기를 감소시킨다.

![image](https://user-images.githubusercontent.com/64063767/152646891-d8f1258b-72be-4ed0-9047-061d4aee0827.png)

### 3.2 L1 Regularization

- **W의 절댓값**에 대해 페널티를 부여하는 규제 방식
- L1 규제를 적용한 선형 회귀를 **라쏘(Lasso) 회귀 모델**이라 한다.
- L1 규제를 적용하면 영향력이 크지 않은 불필요한 피처의 회귀 계수 값을 급격하게 감소시켜 0으로 만들고 제거한다.
- L1 규제는 통해 적절한 피처들만 회귀 모델에 포함시키는 Feature Selection 역할을 한다.

<img src="https://user-images.githubusercontent.com/64063767/152647482-baa300e0-e440-42ea-8b6f-7a7e93d06b0f.png" alt="image" style="zoom:67%;" />

### 3.3 ElasticNet

- L2, L1 규제를 함께 결합한 모델
- 주로 피처가 많은 데이터 세트에서 적용되며, L1 규제로 피처의 개수를 줄임과 동시에 L2 규제로 계수 값의 크기를 조정한다.

### Regularization Summary

- L1 Regularization, L2 Regularization 모두 **Overfitting(과적합)을 방지**하기 위해 사용된다.
- L1은 Sparse Model에 적합하다.
- L1의 경우 미분 불가능한 점이 있기 때문에 Gradient-base learning에는 주의가 필요하다.

<br/>

## References

- [선형 회귀 모델에서 '선형'이 의미하는 것은 무엇인가?](https://brunch.co.kr/@gimmesilver/18)

- [회귀분석 - 단순선형 회귀분석 이론](https://blog.naver.com/PostView.nhn?blogId=winddori2002&logNo=221676654945)

- [릿지 회귀와 라쏘 회귀 쉽게 이해하기](https://rk1993.tistory.com/entry/Ridge-regression%EC%99%80-Lasso-regression-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
- [L1, L2 Regularization 개념, 용도와 차이](https://light-tree.tistory.com/125)