# ML Algorithm Based on Decision Tree

![image](https://user-images.githubusercontent.com/64063767/114155696-b94ffc80-995c-11eb-87de-49b4344af74b.png)

## 1. Decision Tree

<img src="https://user-images.githubusercontent.com/64063767/109497901-14790e80-7ad6-11eb-8fae-9238881d293d.png" alt="image" style="zoom:67%;" />

Decision Tree(의사결정나무)는 마치 스무고개처럼 YES/NO의 이진 노드를 겹쳐서 질문을 이어가며 학습하는 Supervised Learning(지도학습) 모델 중 하나이다. Classification(분류)과 Regression(회귀) 분석에 모두 적용할 수 있다.

이해하기는 쉬우나 트리에 가지가 너무 많다면 Overfitting(과적합)이 되기 쉽다는 단점이 있어서 이를 막기 위한 전략으로 Pruning(가지치기) 기법을 활용하기도 한다. 즉, 최대 깊이나 끝노드인 Terminal node(Leaf node)의 최대 개수, 혹은 하나의 노드가 분할하기 위한 최소 데이터 수를 제한하는 것이다.

```python
min_sample_split = 10 # 한 노드에 10개의 데이터가 있다면 그 노드는 더이상 분기를 하지 않는다
max_depth = 4 # 깊이가 4보다 크게 가지를 치지 않는다
```

<br/>

### 1.1 정보 균일도 측정

Decision Tree에서 노드를 분할하는 기준으로 **정보이득** 또는 **지니계수**를 이용한다.

#### 1.1.1 정보이득(Information Gain)

정보이득은 엔트로피 개념을 기반으로 한다. 엔트로피는 데이터 집합의 혼잡도를 의미하는데, 서로 다른 값이 섞여 있으면 엔트로피가 높고, 같은 값이 섞여 있으면 엔트로피가 낮다. 정보이득 지수는 (1-Entropy 지수) 값이다. 결정트리는 이 정보이득 지수로 분할 기준을 정한다. 즉, **정보이득이 높은 변수를 기준으로 분할한다.**

#### 1.1.2 지니계수(Gini Coefficient)

원래 경제학에서 불평등 지수를 나타낼 때 사용되는 계수이다. 0이 가장 평등하고, 1로 갈수록 불평등하다. 지니계수가 낮을 수록 데이터 균일도가 높은 것으로 해석되어 **지니 계수가 낮은 변수를 기준으로 분할한다.**

<br/>

### 1.2 장점

- 만들어진 모델을 쉽게 시각화할 수 있어서 비전문가도 이해하기 쉽다.
- **데이터의 스케일에 구애받지 않는다는 것**. 각 특성이 개별적으로 처리되어 데이터를 분할하기 때문에, 데이터 스케일의 영향을 받지 않으므로 Decision Tree 기반 알고리즘(RandomForest, XGBoost, LightGBM 등)에서는 정규화나 표준화같은 데이터 전처리 과정이 필요 없다.
- 특히, 특성의 스케일이 서로 다르거나 이진 특성과 연속적인 특성이 혼합되어 있을 때에도 잘 작동한다.
- 학습이 끝난 결정 트리의 작업속도가 매우 빠르다.
- 결정 트리 모델이 어떻게 훈련되었는지 경로의 해석이 가능하다.

### 1.3 단점

- 사전 가지치기를 사용함에도 **과대적합(Overfitting)**되는 경향이 있어 모델의 일반화 성능이 좋지 않다는 것이다.
- 이러한 단일 결정 트리의 단점을 보완한 것이 결정 트리의 **앙상블 방법**이다.

<br/>

## 2. Ensemble Model

여러개의 Weak Classifier(약분류기)를 결합하여 하나의 모델로 예측한 것보다 정확한 Strong Classifer(강분류기)를 만들어 더 좋은 성능을 내게하는 머신러닝 기법이다.

![image](https://user-images.githubusercontent.com/64063767/151815222-85fbb36f-5e4f-47a4-b4ec-ac4a1ff7792c.png)

### 2.1 RandomForest

기존 Decision Tree의 과적합 문제를 해결하기 위해 등장한 Bagging 방식의 알고리즘이다.

Bagging(Bootstrap Aggregation)은 서로 독립적으로 랜덤복원추출한 Bootstrap 표본들로 각각 여러개의 예측모델들을 만드는 학습 방식이다. 학습된 모델로부터 예측 결과들을 집계하여 최종 결과값을 구한다.

![RandomForest](https://user-images.githubusercontent.com/64063767/151813895-6ef28f85-b689-4db7-8db4-54143791a220.png)

### 2.2 XGBoost

**Boosting**

Boosting 알고리즘은 여러 개의 약한 학습기(weak learner)를 순차적으로 학습-예측하면서 **잘못 예측한 데이터에 가중치 부여**를 통해 오류를 개선해 나가는 학습 방식이다.

Boosting 알고리즘으로 GBM, AdaBoost, XGBoost 등이 있다.

GBM은 AdaBoost와 유사하지만 경사하강법(Gradient Descent)을 통해 가중치를 업데이트한다는 큰 차이가 있다.

Boosting 알고리즘은 순차적으로 학습하기에 학습 시간이 매우 오래 걸리는 단점이 있다. 이러한 단점을 극복하기 위해 병렬학습이 가능하도록 구현한 머신러닝 라이브러리가 XGBoost이다. XGBoost는 동일 데이터셋에 대해 RandomForest보다 학습 속도가 빠르다는 장점이 있다.

![XGBoost](https://user-images.githubusercontent.com/64063767/151815515-c90ebfab-d64a-459f-8170-be676f937cf0.png)

<br/>

## References

- [결정 트리](https://kolikim.tistory.com/22)

- [앙상블 학습: 배깅과 부스팅](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-11-%EC%95%99%EC%83%81%EB%B8%94-%ED%95%99%EC%8A%B5-Ensemble-Learning-%EB%B0%B0%EA%B9%85Bagging%EA%B3%BC-%EB%B6%80%EC%8A%A4%ED%8C%85Boosting)
- [XGBoost Algorithm](https://towardsdatascience.com/https-medium-com-vishalmorde-xgboost-algorithm-long-she-may-rein-edd9f99be63d)
- [XGBoost](https://dining-developer.tistory.com/3)