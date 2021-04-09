# Decision Tree 기반 머신러닝 알고리즘

## Decision Tree(의사결정나무)

<img src="https://user-images.githubusercontent.com/64063767/109497901-14790e80-7ad6-11eb-8fae-9238881d293d.png" alt="image" style="zoom:67%;" />

> Decision Tree(의사결정나무)는 마치 스무고개처럼 YES/NO의 이진 노드를 겹쳐서 질문을 이어가며 학습하는 Supervised Learning(지도학습) 모델 중 하나이다. Classification(분류)과 Regression(회귀) 문제에 모두 적용할 수 있다.
>
> 이해하기는 쉬우나 트리에 가지가 너무 많다면 Overfitting(과적합)이 되기 쉽다는 단점이 있어서 이를 막기 위한 전략으로 Pruning(가지치기) 기법을 활용하기도 한다. 즉, 최대 깊이나 끝노드인 Terminal node(Leaf node)의 최대 개수, 혹은 하나의 노드가 분할하기 위한 최소 데이터 수를 제한하는 것이다.
>
> ```python
> min_sample_split = 10 # 한 노드에 10개의 데이터가 있다면 그 노드는 더이상 분기를 하지 않는다
> max_depth = 4 # 깊이가 4보다 크게 가지를 치지 않는다
> ```



## Ensemble Learning(앙상블)

[앙상블 학습: 배깅과 부스팅](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-11-%EC%95%99%EC%83%81%EB%B8%94-%ED%95%99%EC%8A%B5-Ensemble-Learning-%EB%B0%B0%EA%B9%85Bagging%EA%B3%BC-%EB%B6%80%EC%8A%A4%ED%8C%85Boosting)

> 여러개의 Weak Classifier(약분류기)를 결합하여 하나의 모델로 예측한 것보다 정확한 Strong Classifer(강분류기)를 만들어 더 좋은 성능을 내게하는 머신러닝 기법이다.

- Bagging
- Boosting 



## RandomForest



## XGBoost

[XGBoost Algorithm](https://towardsdatascience.com/https-medium-com-vishalmorde-xgboost-algorithm-long-she-may-rein-edd9f99be63d)

[XGBoost](https://dining-developer.tistory.com/3)

![image](https://user-images.githubusercontent.com/64063767/114155696-b94ffc80-995c-11eb-87de-49b4344af74b.png)