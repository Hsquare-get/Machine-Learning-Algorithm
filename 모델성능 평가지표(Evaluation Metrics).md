# Evaluation Metrics

## Evaluation Metrics 종류

| Regression Model                                             | Classification Model                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| MSE<br />RMSE<br />RMSLE<br />CVRMSE<br />MAE<br />MAPE<br />sMAPE<br />mMAPE<br />R2 Score(R Squared) | Accuracy<br />Precision<br />Recall<br />F1 Score<br />Fall-out<br />Log loss<br />Cost Matrix Gain<br />Cumulative Lift Chart |

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

- 이상치에 robust하다. (이상치에 영향을 적게 받는 통계량을 **robust한 통계량**이라 함 )
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

