# 모델성능 평가지표(Evaluation Metrics)

- References
  - [모델성능 평가지표 (회귀모델, 분류모델)](https://rk1993.tistory.com/entry/%EB%AA%A8%EB%8D%B8-%EC%84%B1%EB%8A%A5-%ED%8F%89%EA%B0%80-%EC%A7%80%ED%91%9C-%ED%9A%8C%EA%B7%80-%EB%AA%A8%EB%8D%B8-%EB%B6%84%EB%A5%98-%EB%AA%A8%EB%8D%B8)
  - [분류성능평가지표](https://sumniya.tistory.com/26)

---

<img src="https://user-images.githubusercontent.com/64063767/119266226-e282ce80-bc24-11eb-9fe3-db31d198cef1.png" alt="image" style="zoom:67%;" />

## Evaluation Metrics 종류

| Regression Model                                             | Classification Model                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| MSE<br />RMSE<br />RMSLE<br />CVRMSE<br />MAE<br />MAPE<br />sMAPE<br />mMAPE<br />R2 Score(R Squared) | Accuracy<br />Precision<br />Recall<br />F1 Score<br />Fall-out<br />Log loss<br />Cost Matrix Gain<br />Cumulative Lift Chart<br />ROC curve & AUC |

<br/>

## Regression Model

### MSE (Mean Squared Error)

> 실제값과 예측값의 차이 제곱의 평균

- 실제값과 예측값의 차이 면적의 합으로 이상치에 민감하여 이상치가 존재하면 수치가 많이 증가한다.
- 지표 자체가 직관적이고 단순하다.
- 단위에 의존적이다.
- 에러를 제곱하기 때문에, 1미만의 에러는 더 작아지고 그 이상의 에러는 더 커진다.

<br/>

### RMSE (Root Mean Square)

> MSE에 루트를 씌운 것

- 오류 지표를 실제 값과 같은 단위로 다시 변환하여 해석을 쉽게한다.
- 제곱근 Root를 씌워 이상치에는 더 큰 패널티를 부여함으로써 왜곡을 줄일 수 있다.
- 이상치의 영향에 민감한 머신러닝 모델에서 RMSE를 성능지표로 자주 쓰이는 이유이기도 하다.

<br/>

### RMSLE (Root Mean Square Logarithmic Error)

> RMSE에 로그를 취해준 것

- 이상치에 robust하다. (이상치에 영향을 적게 받는 통계량을 **robust한 통계량**이라 함)
  RMSLE는 이상치가 있더라도 값의 변동폭이 크지 않다.
- RMSE와 달리 실제값과 예측값의 상대적 오차를 측정해준다.
- Under Estimation에 큰 패널티를 부여한다. 즉, 예측값이 실제값보다 작을 때 패널티 부여.

<br/>

### CVRMSE (Coefficient of Variation of the Root Mean Square Error)

> CV(Coefficient of Variation, 변동계수): 표준편차/평균, 측정단위가 서로 다른 자료를 비교하고자 할 때 쓰임
>
> CVRMSE: 평균제곱근오차의 변동계수

- RMSE를 정규화한 것.
- 개별 데이터 포인트에서 관찰된 오류가 아니라 평균 오류를 정량화 한다.

<br/>

### MAE (Mean Absolute Error)

> 실제값과 예측값의 차이를 모두 더한 것

- 절대값을 취하기 때문에 가장 직관적으로 알 수 있는 지표이다.
- MSE보다 이상치에 robust하다.

- 절대값을 취하기 때문에 모델이 underperformance인지 overperformance인지 알 수 없다.

<br/>

### MAPE (Mean Absolute Percentage Error)

> 오차가 실제값에서 차지하는 정도를 나타내는 지표
>
> 예측값과 실제값의 차이를 실제값으로 나누어 예측 모델이 실제값과 얼마나 유사한지를 비율로 계산한 지표

- MAE와 마찬가지로 MSE보다 이상치에 robust하다.
- MAE와 같은 단점을 가진다.
- 모델에 대한 편향 bias가 존재한다.
  - 이 단점에 대응하기 위해 MPE도 추가로 확인하는 것이 좋다.
  - 실제값이 0일 경우 정의할 수 없으며 실제값이 0에 가까운 작은 경우 MAPE가 급격하게 높아지는 문제를 가지고 있다.
  - 실제값과 예측값의 합이 동일하고 차이가 동일한 경우에도 MAPE가  다른 값을 가지는 문제점이 있다.
    이에 대한 개선 방법으로 sMAPE(Symmetric Mean Absolute Percentage Error) 지표를 활용한다.

<br/>

### sMAPE (Symmetric Mean Absolute Percentage Error)

> 예측값과 실제값의 합과 차의 비율로 얼마나 정확하게 예측했는지를 판단하는 지표

- 예측값이 실제값보다 큰 경우(과대예측)와 실제값보다 작은 경우(과소예측) 동등하게 다루지 않는다는 문제점이 있다.
- 실제값과 예측값의 부호가 다른 경우, 오차가 항상 최대값으로 나오게되는 문제점이 있다.

<br/>

### mMAPE (Maximum Mean Absolute Percentage Error)

> MAPE, sMAPE가 가지는 문제점을 해결하는 지표

- 최대 절대값이 1보다 작은경우 실제값과 예측값의 차이를 평가 값으로 계산한다.
- MAPE 수식의 분모에서 실제값을 사용하는 대신 최대 절대값을 사용한다.
- 최대 절대값이 1보다 작으면 분모를 제거하여 실제값이 0일 경우 정의되지 않는 문제와 매우 작은 값일 경우 과대측정되는 문제를 해결할 수 있다.

<br/>

### R2 Score / R Squared (Coefficient of Determination, 결정계수)

> 추정한 선형 모형이 주어진 자료에 얼마나 적합한지를 재는 척도
>
> 실제값의 변동량 중에서 적용한 모형으로 설명가능한 부분의 비율 (1에 가까울수록 설명력이 좋다)

- 다른 성능지표인 RMSE나 MAE는 데이터의 범위에 따라서 값이 다르기 때문에 절대값만 보고 바로 성능을 판단하기가 어려운데, 결정계수의 경우 상대적인 성능이기 때문에 이를 직관적으로 알 수 있다.

<br/>

## Classification Model

### Confusion Matrix (오차행렬)

![image](https://user-images.githubusercontent.com/64063767/119266403-a4d27580-bc25-11eb-8125-7333b3200438.png)

### Accuracy (정확도)

> 전체에서 정답을 맞춘 비율

- Bias에 관해 단점을 가진다. (**정확도 역설**)
- 실제 데이터에 Negative 비율이 너무 높아서 희박한 가능성으로 발생할 상황에 대해 제대로된 분류를 해주는지 평가해줄 지표는 Precision(정밀도)와 Recall(재현율)이다.

<br/>

### Recall (재현율)

> 실제 True인 것 중에서 모델이 True라고 예측한 것의 비율

- 실제 데이터에서 Negative 비율이 너무 높아서 희박한 가능성으로 발생할 상황에 유용하다.
- 언제나 True만 답하는 분류기가 있다면 Accuracy는 실제 True인 경우에 대해서만큼은 정확하게 맞힐 수 있기 때문에 Recall은 1이 된다.

<br/>

### Precision (정밀도)

> True라고 분류한 것 중에서 길제 True인 것의 비율

- 언제나 True만 답하는 분류기가 있다면 Recall은 1로 나오겠지만, Precision은 0에 가깝게 나온다.
- **Recall과 Precision은 서로 Trade Off 관계**
- Recall과 Precision 모두 유용한 지표이긴 하지만 충분히 성능을 표현하기에는 한계가 있다. 그래서 이를 보완한 것이 Recall과 Precision의 조화평균 F1 Score다.

<br/>

### F1 Score

> Precision과 Recall의 조화평균으로 F1 Score가 높아야 성능이 좋음

- 산술평균을 사용하지 않는 이유는 Precision과 Recall 둘 중 하나가 0에 가깝게 낮을 때 지표에 그것이 잘 반영되도록, 즉 두 지표를 모두 균형있게 반영하여 모델의 성능이 좋지 않다는 것을 잘 확인하기 위해 조화평균을 사용한다.
