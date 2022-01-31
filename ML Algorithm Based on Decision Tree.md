# Machine Learning Algorithm Based on Decision Tree

## Decision Tree(의사결정나무)

<img src="https://user-images.githubusercontent.com/64063767/109497901-14790e80-7ad6-11eb-8fae-9238881d293d.png" alt="image" style="zoom:67%;" />

Decision Tree(의사결정나무)는 마치 스무고개처럼 YES/NO의 이진 노드를 겹쳐서 질문을 이어가며 학습하는 Supervised Learning(지도학습) 모델 중 하나이다. Classification(분류)과 Regression(회귀) 분석에 모두 적용할 수 있다.

이해하기는 쉬우나 트리에 가지가 너무 많다면 Overfitting(과적합)이 되기 쉽다는 단점이 있어서 이를 막기 위한 전략으로 Pruning(가지치기) 기법을 활용하기도 한다. 즉, 최대 깊이나 끝노드인 Terminal node(Leaf node)의 최대 개수, 혹은 하나의 노드가 분할하기 위한 최소 데이터 수를 제한하는 것이다.

```python
min_sample_split = 10 # 한 노드에 10개의 데이터가 있다면 그 노드는 더이상 분기를 하지 않는다
max_depth = 4 # 깊이가 4보다 크게 가지를 치지 않는다
```

<br/>

### Pros and Cons

https://kolikim.tistory.com/22

- **장점**
  - 만들어진 모델을 쉽게 시각화할 수 있어서 비전문가도 이해하기 쉽다.
  - **데이터의 스케일에 구애받지 않는다는 것**. 각 특성이 개별적으로 처리되어 데이터를 분할하기 때문에, 데이터 스케일의 영향을 받지 않으므로 Decision Tree 기반 알고리즘(RandomForest, XGBoost, LightGBM 등)에서는 정규화나 표준화같은 데이터 전처리 과정이 필요 없다.
  - 특히, 특성의 스케일이 서로 다르거나 이진 특성과 연속적인 특성이 혼합되어 있을 때에도 잘 작동한다.
  - 학습이 끝난 결정 트리의 작업속도가 매우 빠르다.
  - 결정 트리 모델이 어떻게 훈련되었는지 경로의 해석이 가능하다.

- **단점**
  - 사전 가지치기를 사용함에도 **과대적합(Overfitting)**되는 경향이 있어 모델의 일반화 성능이 좋지 않다는 것이다.
  - 이러한 단일 결정 트리의 단점을 보완한 것이 결정 트리의 **앙상블 방법**이다.

<br/>

## Ensemble Learning(앙상블)

[앙상블 학습: 배깅과 부스팅](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-11-%EC%95%99%EC%83%81%EB%B8%94-%ED%95%99%EC%8A%B5-Ensemble-Learning-%EB%B0%B0%EA%B9%85Bagging%EA%B3%BC-%EB%B6%80%EC%8A%A4%ED%8C%85Boosting)

> 여러개의 Weak Classifier(약분류기)를 결합하여 하나의 모델로 예측한 것보다 정확한 Strong Classifer(강분류기)를 만들어 더 좋은 성능을 내게하는 머신러닝 기법이다.

- Bagging(Bootstrap Aggregating)
  - 서로 독립적으로 랜덤복원추출(random sampling)한 Bootstrap 표본들을 가지고 각각 여러개의 예측모델들이 학습한다. 학습된 모델들로부터 예측 결과들을 집계하여 최종 결과값을 구하는 학습 방식을 Bagging이라 한다.
- Boosting 
  - 서로 독립적이던 Bagging 방식과는 달리 이전모델의 오류를 고려하여 다음모델의 정확도를 높이는 학습방식을 Boosting이라 한다.



## RandomForest



## XGBoost

[XGBoost Algorithm](https://towardsdatascience.com/https-medium-com-vishalmorde-xgboost-algorithm-long-she-may-rein-edd9f99be63d)

[XGBoost](https://dining-developer.tistory.com/3)

![image](https://user-images.githubusercontent.com/64063767/114155696-b94ffc80-995c-11eb-87de-49b4344af74b.png)