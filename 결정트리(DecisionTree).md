# 결정트리(DecisionTree)

<img src="https://user-images.githubusercontent.com/64063767/109497901-14790e80-7ad6-11eb-8fae-9238881d293d.png" alt="image" style="zoom:67%;" />

- Decision Tree(의사결정나무)는 마치 스무고개처럼 YES/NO의 이진 노드를 겹쳐서 질문을 이어가며 학습하는 Supervised Learning(지도학습) 모델 중 하나이다.
- Classification(분류)과 Regression(회귀) 분석에 모두 적용할 수 있다.

- 이해하기는 쉬우나 트리에 가지가 너무 많다면 Overfitting(과적합)이 되기 쉽다는 단점이 있어서 이를 막기 위한 전략으로 Pruning(가지치기) 기법을 활용하기도 한다.
- 즉, 최대 깊이나 끝노드인 Terminal node(Leaf node)의 최대 개수, 혹은 하나의 노드가 분할하기 위한 최소 데이터 수를 제한하는 것이다.

- 선형 회귀분석처럼 간단한 문제에는 잘 맞지만 복잡한 문제에서는 잘 맞지 않는다.

```python
min_sample_split = 10 # 한 노드에 10개의 데이터가 있다면 그 노드는 더이상 분기를 하지 않는다
max_depth = 4 # 깊이가 4보다 크게 가지를 치지 않는다
```

<br/>

## 1. 정보 균일도 측정

Decision Tree에서 노드를 분할하는 기준으로 **정보이득** 또는 **지니계수**를 이용한다.

### 1.1 정보이득(Information Gain)

정보이득은 엔트로피 개념을 기반으로 한다. 엔트로피는 데이터 집합의 혼잡도를 의미하는데, 서로 다른 값이 섞여 있으면 엔트로피가 높고, 같은 값이 섞여 있으면 엔트로피가 낮다. 정보이득 지수는 (1-Entropy 지수) 값이다. 결정트리는 이 정보이득 지수로 분할 기준을 정한다. 즉, **정보이득이 높은 변수를 기준으로 분할한다.**

### 1.2 지니계수(Gini Coefficient)

원래 경제학에서 불평등 지수를 나타낼 때 사용되는 계수이다. 0이 가장 평등하고, 1로 갈수록 불평등하다. 지니계수가 낮을 수록 데이터 균일도가 높은 것으로 해석되어 **지니 계수가 낮은 변수를 기준으로 분할한다.**

<br/>

## 2. 장단점

### 2.1 장점

- 만들어진 모델을 쉽게 시각화할 수 있어서 비전문가도 이해하기 쉽다.
- **데이터의 스케일에 구애받지 않는다는 것**. 각 특성이 개별적으로 처리되어 데이터를 분할하기 때문에, 데이터 스케일의 영향을 받지 않으므로 Decision Tree 기반 알고리즘(RandomForest, XGBoost, LightGBM 등)에서는 정규화나 표준화같은 데이터 전처리 과정이 필요 없다.
- 특히, 특성의 스케일이 서로 다르거나 이진 특성과 연속적인 특성이 혼합되어 있을 때에도 잘 작동한다.
- 학습이 끝난 결정 트리의 작업속도가 매우 빠르다.
- 결정 트리 모델이 어떻게 훈련되었는지 경로의 해석이 가능하다.

### 2.2 단점

- 사전 가지치기를 사용함에도 **과대적합(Overfitting)**되는 경향이 있어 모델의 일반화 성능이 좋지 않다는 것이다.
- 이러한 단일 결정 트리의 단점을 보완한 것이 결정 트리의 **앙상블 방법**이다.

<br/>

## References

- [결정 트리](https://kolikim.tistory.com/22)