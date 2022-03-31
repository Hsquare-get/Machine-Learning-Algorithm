# 앙상블(Ensemble)

여러개의 Weak Classifier(약분류기)의 예측값을 투표나 평균을 내어 하나의 모델로 예측한 것보다 정확한 Strong Classifier(강분류기)를 만들어 더 좋은 성능을 내게하는 머신러닝 기법이다.

## 0. DecisionTree 기반 알고리즘 발전사

![image](https://user-images.githubusercontent.com/64063767/114155696-b94ffc80-995c-11eb-87de-49b4344af74b.png)

## 1. Bagging(배깅)

<img src="https://user-images.githubusercontent.com/64063767/154631867-fdd9666a-b28d-4dd1-8d0d-10315e5b6339.png" alt="image" style="zoom:67%;" />

- **Bagging(Bootstrap Aggregating)**은 전체 데이터셋에서 Bootstrap 표본들을 생성하여 각각의 Bootstrap마다 예측모델을 만들고 결합하여 최종 예측모델을 만드는 방법이다.

- **Bootstrap**은 전체 데이터셋에서 서로 독립적으로 랜덤복원추출한 표본을 의미한다.
- 기존 DecisionTree의 과적합 문제를 해결하기 위해 등장하였다.
- **Voting**은 여러 개의 모델로부터 산출된 결과를 **다수결**에 의해서 최종 결과를 선정한다.
- Bagging에서는 **가지치기를 하지 않고 최대로 성장한 DecisionTree들을 활용**한다.

<br/>

### 1.1 RandomForest

![RandomForest](https://user-images.githubusercontent.com/64063767/151813895-6ef28f85-b689-4db7-8db4-54143791a220.png)

- RandomForest는 Bagging 방식의 알고리즘 중 하나.

- 분산이 크다는 DecisionTree의 특징을 고려하여 Bagging과 Boosting보다 더 많은 무작위성을 주어 **Weak Learner**를 생성하고 이를 **선형결합하여 최종 예측모델을 만드는 방법**이다.

<br/>

## 2. Boosting(부스팅)

<img src="https://user-images.githubusercontent.com/64063767/118439225-80a3ff80-b720-11eb-9b27-9119fd55200f.png" alt="image"  />

![image](https://user-images.githubusercontent.com/64063767/151815222-85fbb36f-5e4f-47a4-b4ec-ac4a1ff7792c.png)

- Boosting 알고리즘은 여러 개의 약한 학습기(weak learner)를 **순차적으로 학습-예측**하면서 **잘못 예측한 데이터에 가중치 부여**를 통해 오류를 개선해 나가는 학습 방식이다.
- Boosting은 Additive model 중 하나이다. Additive model은 비모수 회귀, 즉 함수 형태를 가정하지 않는 회귀모형을 의미한다. 부스팅이 이러한 Additive model에 속한다는 것은 결국은 회귀식 형태로 해석이 가능하다는 뜻이다.
- Boosting 알고리즘으로 GBM, AdaBoost, XGBoost, LGBM, CatBoost 등이 있다.

<br/>

### 2.1 AdaBoost

<img src="https://user-images.githubusercontent.com/64063767/154635045-e4239029-d25d-4f2d-821a-ec8a7032dac1.png" alt="image" style="zoom: 33%;" />

- AdaBoost는 약한 학습기 (Weak Learner)로 구성되어 있으며, 약한 학습기는 stump의 형태이다.
- stump는 노드 하나에 두개의 리프(leaf)를 지닌 트리를 의미한다.
- training set의 모든 관측치에 대해 weight = 1/n로 초기화시키고 시작한다.
- 그 후로는 오분류한 데이터에 대해 weight를 갱신하여 데이터셋 자체를 수정하면서(modified dataset) 학습을 진행한다.
- 각 stump의 error는 다음 stump의 결과에 영향을 준다.
- 어떤 stump는 다른 stump보다 가중치가 높다.
- 여러 stump가 순차적으로 연결되어 최종 결과를 도출한다.

<br/>

### 2.2 GBM (Gradient Boosting Machine)

<img src="https://user-images.githubusercontent.com/64063767/154633310-bff80e85-2fb6-4b0f-baef-b7064f4018a8.png" alt="image"  />

<img src="https://user-images.githubusercontent.com/64063767/118443383-c82d8a00-b726-11eb-93ec-c6c47c96267c.png" alt="image" style="zoom:67%;" />

- GBM은 AdaBoost와 유사하지만 경사하강법(Gradient Descent)을 통해 가중치를 업데이트한다는 큰 차이가 있다.
- GBM은 stump나 tree가 아닌 하나의 leaf(single leaf)부터 시작한다.
- GBM은 residual을 줄이는 방향으로 weak learner들을 결합해 나간다.
- 위 그림의 tree1, tree2, tree3이 각각 weak learner가 되고, 각 모델에서 실제값과 예측값의 차이(residual)를 다음 모델에서 fitting 시킨다.
- GBM은 residual을 줄이는 방향으로 weak learner를 결합해 강력한 성능을 자랑하지만, 해당 train data에 residual을 계속 줄이게됨으로 과적합(overfitting)되기 쉽다는 문제점이 있다.

<br/>

### 2.3 XGBoost

<img src="https://user-images.githubusercontent.com/64063767/151815515-c90ebfab-d64a-459f-8170-be676f937cf0.png" alt="XGBoost" style="zoom:67%;" />

![image](https://user-images.githubusercontent.com/64063767/118444978-ce246a80-b728-11eb-9532-1e6598a45d48.png)

- Boosting 알고리즘은 순차적으로 학습하기에 학습 시간이 매우 오래 걸리는 단점이 있다.
- 이러한 단점을 극복하기 위해 **병렬학습**이 가능하도록 구현한 머신러닝 라이브러리가 XGBoost이다.
- GBM의 과적합 문제를 개선하기 위해 GBM에 regularization term을 추가한 알고리즘이 XGBoost이다.
- XGBoost의 regularization term은 tree 복잡도가 증가할수록 loss에 페널티를 주는 방식으로 overfitting을 막고 있다.
- XGBoost는 동일 데이터셋에 대해 RandomForest보다 학습 속도가 빠르다는 장점이 있다.

<br/>

### 2.4 LightGBM

![image](https://user-images.githubusercontent.com/64063767/151936289-60c7b1a4-b3ec-4d10-b261-603a87479689.png)

- XGBoost 대비 더 빠른 학습과 예측 수행시간이 가능하며 더 작은 메모리 사용량으로 학습이 가능하다.

- Category 변수의 자동 변환과 최적 분할이 가능하다.

- 균형트리분할(Level Wise) 방식인 XGBoost와 달리 LightGBM은 리프중심으로 트리분할(leaf wise)한다.
- 과적합에 민감하여, 대량의 학습데이터를 필요로한다.

<br/>

### 2.5 CatBoost

- 잔차 추정의 분산을 최소로 하면서 bias를 피하는 boosting 기법이다.
- 관측치를 포함한 채로 boosting 하지않고, 관측치를 뺀 채로 학습해서 그 관측치에 대한 unbiased residual 구하고 학습하는 형태이다.
- Category 변수가 많은 경우 잘 맞는다고 알려짐.
- Category 변수를 one-hot encoding이 아니라 수치형으로 변환한다.

<br/>

## 3. Stacking(스태킹)

![Stacking](https://user-images.githubusercontent.com/64063767/152153691-7c9f6ab3-742b-42cc-b034-4bd6d25c9dc0.png)

- 여러 모델들의 예측값을 기반으로 **메타 모델이 재학습**하여 예측하는 기법

- 예를 들어 KNN, Logistic Regression, RandomForest, XGBoost의 서로 다른 알고리즘을 활용해서 메타 모델(최종 모델)로 선정한 LightGBM을 재학습시킬 수 있다.

- 성능이 무조건 좋아지지 않기 때문에 현실 모델에서도 많이 사용되지는 않는다. 다만, 성능이 올라가는 경우가 더러 있기 때문에 캐글이나 데이콘 같은 미세한 성능차이로 승부를 결정하는 대회에서 주로 사용된다. 특히 기반 모델로 4개 이상을 선택해야 좋은 결과를 기대할 수 있다고 한다.

| 메타 모델의 학습 데이터                                      | 메타 모델의 테스트 데이터                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image](https://user-images.githubusercontent.com/64063767/152162397-74ed146d-b180-47c7-b291-ef8bf34c0bca.png) | ![image](https://user-images.githubusercontent.com/64063767/152162447-ce64bd0b-d747-4cc8-93fa-e15f2c382d4d.png) |

<br/>

## References

- [Boosting Algorithm](https://hyunlee103.tistory.com/25)
- [XGBoost Algorithm](https://towardsdatascience.com/https-medium-com-vishalmorde-xgboost-algorithm-long-she-may-rein-edd9f99be63d)
- [XGBoost](https://dining-developer.tistory.com/3)
- [머신러닝 - 11.앙상블 학습: 배깅과 부스팅](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-11-%EC%95%99%EC%83%81%EB%B8%94-%ED%95%99%EC%8A%B5-Ensemble-Learning-%EB%B0%B0%EA%B9%85Bagging%EA%B3%BC-%EB%B6%80%EC%8A%A4%ED%8C%85Boosting)
- [머신러닝 - 14.에이다 부스트](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-14-AdaBoost)
- [머신러닝 - 15.그레디언트 부스트](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-15-Gradient-Boost)
- [XGBoost vs GBM](https://m.blog.naver.com/nicolechae0627/221811579005#)
- [XGBoost, LightGBM, CatBoost 정리 및 비교](https://statinknu.tistory.com/33)
- [CatBoost란? unbiased boosting with categorical features-1](https://data-newbie.tistory.com/131)
- [Catboost 주요 개념과 특징 이해하기](https://dailyheumsi.tistory.com/136)
- [What's so special about CatBoost?](https://hanishrohit.medium.com/whats-so-special-about-catboost-335d64d754ae)

- [스태킹(Stacking) 완벽 정리](https://hwi-doc.tistory.com/entry/%EC%8A%A4%ED%83%9C%ED%82%B9Stacking-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)