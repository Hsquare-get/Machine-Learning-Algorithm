# Cross-Validation(교차검증)

![image](https://user-images.githubusercontent.com/64063767/108304413-55764680-71eb-11eb-83ac-ce2b593fcfdb.png)

<br/>

| ![Cross-Validatoin](https://t1.daumcdn.net/cfile/tistory/994042405E24E8081C) | ![image](https://user-images.githubusercontent.com/64063767/119229320-69b34200-bb52-11eb-85f6-4fff0a018815.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

dataset을 모델 훈련에 사용할 `training set`와 일반화 성능을 추정하는데 사용할 `test set`으로 나눈다. 그리고 예측 성능을 높이기 위해 **hyper parameter를 튜닝하고 비교**해야하는데, 이때 모델 선택에 같은 test set를 반복해서 재사용하면 이는 training set의 일부가 되는 셈이고 모델의 **overfitting(과대적합) 요인**이 될 수 있다.

그러므로 dataset을 `training set`, `validation set`, `test set`으로 적절하게 나눈다.

(If any **parameters need to be tuned**, we split the **training set into a training subset and a validation set**)

<br/>

### 0. Holdout Method

![image](https://user-images.githubusercontent.com/64063767/108305117-b6eae500-71ec-11eb-9154-5984c29f2215.png)

홀드아웃 방법은 일반적으로 사용하는 데이터셋을 train과 validation으로 나눈다. 보통 8:2로 나누지만 7:3, 9:1 비율로도 나누기도 한다. (dataset이 천만개 이상의 단위라면 극단적으로 validation set의 크기를 줄일 수도 있다)

training set / validation set / test set 세 부분으로 나눌땐 6:2:2의 비율로 나누기도 한다.

<hr/>

#### training / validation / test set으로 모델을 만들면되지 교차 검증은 왜 필요할까?

고정적인 training set으로 모델을 만드는 경우 overfitting(과대적합)이 나타날 수 있습니다. 이러한 문제를 해결하고, 충분한 정확도로 일반화시킬 수 있는 모델을 만들기 위해 교차검증을  활용하여 모델을 평가한다.

교차검증 방법에는 `K-fold Cross Validation` / `Leave-p-out Cross Validation` / `Leave-one-out Cross Validation` 등이 있다. 

<br/>

## 1. Traditional Cross-Validation

### (1) K-fold Cross Validation

![image](https://user-images.githubusercontent.com/64063767/108306290-32e62c80-71ef-11eb-851c-d3fd3aac6d0a.png)

![image](https://user-images.githubusercontent.com/64063767/108306479-940e0000-71ef-11eb-8030-f993a28057d3.png)

K-겹 교차검증은 가지고 있는 데이터를 K개의 그룹으로 나누고, 그 그룹 중에서 하나를 추출하여 validation set으로 사용하는 것이다. 그리고 이 과정을 **K번 반복하여 나온 결과값의 평균으로 검증 결과값**으로 사용한다.

##### 장점

1. 모든 데이터셋을 훈련에 활용할 수 있다.
   - 정확도를 향상시킬 수 있다.
   - 데이터 부족으로 인한 `underfitting`을 방지할 수 있다.
2. 모든 데이터셋을 평가에 활용할 수 있다.
   - 평가에 사용되는 데이터 편중을 막을 수 있다.
   - 특정 평가 데이터셋에 `overfitting`되는 것을 방지할 수 있다.
   - 평가 결과에 따라 좀 더 일반화된 모델을 만들 수 있다.

##### 단점

- Iteration 횟수가 많아지기 때문에 모델 훈련/평가 시간이 오래걸린다.

<br/>

### (2) Leave-p-out Cross Validation

![image](https://user-images.githubusercontent.com/64063767/108307451-1ea32f00-71f1-11eb-9c1a-1151537f34f2.png)

Leave-p-out 교차검증은 가지고 있는 데이터셋에서 p개의 데이터를 추출하여 validation set으로 활용하는 방법이다. 이 방법 또한 계산 시간이 오래 걸린다는 단점이 있다.

![image](https://user-images.githubusercontent.com/64063767/108309668-4dbb9f80-71f5-11eb-8f74-ab977487505e.png)

validation set을 구성할 수 있는 경우의 수(훈련 및 검증에 소요되는 Iteration 횟수)

<br/>

### (3) Leave-one-out Cross Validation (LOOCV)

![image](https://user-images.githubusercontent.com/64063767/108307051-c10ee280-71f0-11eb-8101-dee4f926720a.png)

Leave-one-out 교차검증은 Leave-p-out 교차검증에서 p=1일 때의 경우를 말한다. Leave-p-out 교차검증 보다 계산시간에 대한 부담은 줄이고, 더 좋은 결과를 얻을 수 있기 때문에 선호되는 교차검증 방법 중 하나이다. 검증에 사용되는 validation set의 개수가 적어진 만큼 모델 훈련에 사용되는 데이터의 개수는 늘어난다. 모델 검증에 희생되는 데이터 개수가 단 하나이기 때문에, 나머지 모든 데이터를 모델 훈련에 사용할 수 있다는 것이 장점이다.

<br/>

## 2. Time Series Nested Cross Validation

- References

  - [Cross Validation in Time Series](https://medium.com/@soumyachess1496/cross-validation-in-time-series-566ae4981ce4)

  - [Time Series Nested Cross-Validation](https://towardsdatascience.com/time-series-nested-cross-validation-76adba623eb9)

<br/>

### (1) Why is Cross-Validation Different with Time Series?

#### a. Temporal Dependencies

- 시계열 데이터 경우 **Data Leakage** 문제를 방지하기 위해 k-fold 교차검증을 사용을 주의해야한다.

#### b. Arbitrary Choice of Test Set

- test set가 임의적으로 선택되면 test set error가 독립적인 test set에서 잘못된 추정을 의미할 수 있기 때문에 **Nested Cross-Validation** 방법을 활용한다.

- Nested Cross-Validation(중첩교차검증)으로 실제 오차에 대해 편향을 완화시킬 수 있다.

<br/>

### (2) Nested Cross-Validation

![image](https://user-images.githubusercontent.com/64063767/119229802-8e101e00-bb54-11eb-924f-0f72175a74a0.png)

#### a. Predict Second Half

![Predict Second Half](https://miro.medium.com/max/700/1*bkHYVCA4uD3k4FieJ-Nfjw.png)

#### b. Day Forward-Chaining

![Day Forward Chaining](https://miro.medium.com/max/700/1*gYTT2d-Suszciijr10l7iQ.png)

<br/>

### (3) Methods for Time Series Cross-Validation

| Image                                                        | Method                               | Split | Pros                                                         | Cons                                                         |
| ------------------------------------------------------------ | ------------------------------------ | ----- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![Time-Series Split](https://miro.medium.com/max/599/1*XcqvKVTQ6U_zszSD52lSqA.png) | Time-Series Split                    | K     | 1. More splits<br />2. Can inspect how model fares on different days | 1. May create leakage from future data to the model          |
| ![Blocked Cross-Validation](https://miro.medium.com/max/605/1*QJaeOqGfe_vKbpmT882APA.png) | Blocked Cross Validation             | K     | 1. More splits<br />2. Solves data leakage issue             | 1. Maybe very computationally expensive                      |
| ![Predict Second Half](https://miro.medium.com/max/700/1*bkHYVCA4uD3k4FieJ-Nfjw.png) | Regular Predict Second Half          | 1     | 1. Easy to implement<br />2. Produces a single model<br />3. Computationally inexpensive | 1. Arbitary test choice could produce biased estimate        |
| ![Day Forward Chaining](https://miro.medium.com/max/700/1*gYTT2d-Suszciijr10l7iQ.png) | Regular Day Forward Chaining         | K     | 1. More splits<br />2. Can inspect how model fates on different days | 1. Requires consistent number of days in data for each participant<br />2. |
| ![Population Data Day Forward Chaining](https://miro.medium.com/max/700/1*TfN4j6EpTH2d-PbrSc03sQ.png) | Population Data Day Forward Chaining | K     | 1. Most unbiased estimate of error versus other methods<br />2. Can inspect how model fares on different days | 1. Computationally expensive<br />2. Multiple models         |

