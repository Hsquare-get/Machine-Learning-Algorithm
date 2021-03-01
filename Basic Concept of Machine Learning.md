# Basic Concept of Machine Learning

> Machine Learning(기계 학습)은 인공 지능의 한 분야로, 컴퓨터가 학습할 수 있도록하는 알고리즘과 기술을 개발하는 분야를 말한다. (Wikipedia)

<img src="https://user-images.githubusercontent.com/64063767/109463153-e4b31200-7aa7-11eb-8a1a-10f173066c6e.png" alt="image" style="zoom: 67%;" />

- 주어진 데이터를 통해서 입력변수와 출력변수간의 관계를 만드는 함수 f를 만드는 것
- 주어진 데이터 속에서 데이터의 특징을 찾아내는 함수 f를 만드는 것

<br/>

### (1) 지도학습과 비지도학습

#### (i) 지도 학습(Supervised Learning)

- Y = f(X)에 대하여 입력변수(X)와 출력변수(Y)의 관계에 대하여 모델링하는 것 (Y에 대하여 **예측** 또는 **분류**하는 문제)
  - **회귀(Regression)** : 입력변수 X에 대해서 연속형 출력변수 Y를 예측
  - **분류(Classification)** : 입력변수 X에 대해서 이산형 출력변수 Y를 예측
- **Input/Output**
- **Labeled data**

<img src="https://user-images.githubusercontent.com/64063767/109464434-001f1c80-7aaa-11eb-90cc-96983be3d95e.png" alt="image" style="zoom: 67%;" />

<br/>

#### (ii) 비지도 학습(Unsupervised Learning)

- 출력변수(Y)가 존재하지 않고, 입력변수(X)간의 관계에 대해 모델링 하는 것
  - **군집 분석** : 유사한 데이터끼리 그룹화
  - **PCA(Principal Component Analysis, 주성분 분석)** : 독립변수들의 차원을 축소화

- **Input**
- **Unlabeled data**

<img src="https://user-images.githubusercontent.com/64063767/109464599-44122180-7aaa-11eb-8011-30a6bac66c03.png" alt="image" style="zoom: 67%;" />

<br/>

#### (iii) 강화 학습(Reinforcement Learning)

#### (Q-learning)

- 수 많은 시뮬레이션을 통해 현재의 성택이 먼 미래에 보상이 최대가 되도록 학습 (ex. AlphaGo)
- Agent가 action을 취하고 환경에서 보상을 받고 이 보상이 최대가 되도록 최적의 action을 취하는 방법을 학습

<img src="https://user-images.githubusercontent.com/64063767/109465314-5476cc00-7aab-11eb-9205-1b011d6f9302.png" alt="image" style="zoom: 67%;" />

<br/>

### (2) Machine Learning의 종류

#### (Supervised Learning)

#### (i) 선형 회귀분석(Linear Regression)

- 독립변수와 종속변수가 **선형적인 관계에 있다라는 가정하에** 분석

- 직선을 통해 종속변수를 예측하기 때문에 독립변수의 중요도와 영향력을 파악하기 쉬움

- 비선형 관계에 있는 변수들에 대해서는 잘 설명하지 못한다.

<img src="https://user-images.githubusercontent.com/64063767/109468763-6ad35680-7ab0-11eb-8c01-5034ab5c8927.png" alt="image" style="zoom: 67%;" />

<br/>

#### (ii) 의사결정나무(Decision Tree)

- 독립변수의 조건에 따라 종속변수를 분리

- 이해하기 쉬우나 Overfitting(과적합)이 잘 일어난다.
- 선형 회귀분석처럼 간단한 문제에만 잘 맞고 복잡한 문제에선 잘 맞지 않는다.

<img src="C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210301171031242.png" alt="image-20210301171031242" style="zoom: 67%;" />

<br/>

#### (iii) KNN(K-Nearest Neighbor)

- 새로 들어온 데이터의 주변 k개 데이터의 class로 분류하는 기법
  - 여기서 k는 사람이 지정해줘야하는 파라미터로 이를 **Hyper Parameter**라고 한다.
  - k를 어떻게 지정해주느냐에 따라 모델의 성능이 달라질 수 있다.

<img src="https://user-images.githubusercontent.com/64063767/109469583-930f8500-7ab1-11eb-950b-1446de50b7e4.png" alt="image" style="zoom: 67%;" />

<br/>

#### (iv) Neural Network

- 입력(Input layer), 은닉(Hidden layer), 출력(Output layer)층으로 구성된 모형으로서 각 층을 연결하는 노드의 가중치(weight)를 업데이트하면서 학습
- Overfitting이 심하게 일어나고 학습시간이 매우 오래걸린다.

<img src="https://user-images.githubusercontent.com/64063767/109469988-25178d80-7ab2-11eb-90bb-3a5f60717b07.png" alt="image" style="zoom: 67%;" />

<br/>

#### (v) SVM(Support Vector Machine)

- Class 간의 거리(margin)가 최대가 되도록 decision boundary를 만드는 방법
- Neural Network와 달리 SVM은 학습과정내에서 어느정도 오차를 허용하기때문에 decision boundary 직선을 잘 그을 수 있었다.
- 2000년대 초중반 때 많이 사용되었지만 더 좋은 알고리즘들이 나와서 최근에는 잘 쓰이지 않는 경향이 있다.
- SVM은 데이터가 커질수록 학습시간이 매우 오래걸리는 단점이 있다.

<img src="C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210301172027728.png" alt="image-20210301172027728" style="zoom: 67%;" />

<br/>

#### (vi) Ensemble Learning(앙상블 기법)

- 각각의 모델(classifier or base learner or weak classifier)의 Output을 평균을 내거나 다수결 투표를 활용하여 여러개의 모델을 결합하는 모델
- 보통 Decision Tree를 많이 사용하고, 크게 **Bagging, Random Forest, Boosting** 3가지 종류가 있다.

<img src="C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210301172729030.png" alt="image-20210301172729030" style="zoom: 67%;" />

<br/>

#### (Unsupervised Learning)

#### (i) K-means clustering

- Label이 없는 데이터로 k개의 군집을 생성
- k를 얼마로 설정하느냐에 따라서 모델의 성능이 달라진다.
- 데이터가 고차원으로 복잡하게 얽혀있다면 K-means clustering이 잘 맞지 않는다.

<img src="https://user-images.githubusercontent.com/64063767/109471919-d15a7380-7ab4-11eb-872d-8d8de1f0b11c.png" alt="image" style="zoom:67%;" />