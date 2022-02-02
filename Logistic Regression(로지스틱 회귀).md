# Logistic Regression(로지스틱 회귀)

로지스틱 회귀는 예측 변수가 Binary(0 또는 1로 구분할 수 있는 성공/실패, 합격/불합격, 남/여, 스팸/정상)일 때 이진 분류에 활용되는 회귀 알고리즘이다. 

<br/>

## Linear Regression

종속 변수 Y가 성공(1)과 실패(0)인 데이터에 대해 Linear Regression 예측 모델링은 아래와 같다.

![image](https://user-images.githubusercontent.com/64063767/152142792-402eb4b8-f15d-492b-9dcb-5aac3d295f75.png)

Y의 범위가 0~1 이어야 하지만, 연속형 변수를 모델링하는 Linear Regression의 출력 범위는 -∞ ~ ∞ 이다.

<br/>

## Logistic Regression

클래스에 속할 확률을 출력하여 성공과 실패를 예측한다. 이 때 어떤 클래스로 예측할지 결정할 확률 컷오프 값을 임계값(Threshold, Decision Boundary)이라 한다. 기본 값은 0.5이지만 데이터의 특성에 따라 조정할 수 있다.

![image](https://user-images.githubusercontent.com/64063767/152147007-46573fac-695c-4080-9d21-a9908406a869.png)

### Logit transformation

이러한 Linear Regression의 한계를 **로짓 변환**을 통해 해결한다.

Linear Regression에서 *Y = ax+b* 였다면, Logistic Regression에서는 *logit(z) = ax+b* (-∞ ~ ∞)로 가정한다.

- #### **Logit = Log Odds = log(Odds)**

- #### **Odds(승산)**: 성공할 확률/실패할 확률 = P/(1-P)

- #### *Odds ∈ (0,∞)*, *log(Odds) ∈ (-∞,∞)*

- #### *logit(P(Y=1)) = z = ax + b = log(P/(1-P))*

- #### *logit ∈ (-∞,∞)*

- #### ∴ *P(Y=1) = exp(ax+b)/(1+exp(ax+b)) = 1/1+exp-(z) {Sigmoid Function}*

<br/>

## References

- [로지스틱 회귀분석이란?](https://leedakyeong.tistory.com/entry/%EB%A1%9C%EC%A7%80%EC%8A%A4%ED%8B%B1-%ED%9A%8C%EA%B7%80%EB%B6%84%EC%84%9D%EC%9D%B4%EB%9E%80-What-is-Logistic-Regression)

- [로지스틱회귀(Logistic Regression) 쉽게 이해하기](https://hleecaster.com/ml-logistic-regression-concept/)