# Data Analysis Process

![image](https://user-images.githubusercontent.com/64063767/109493173-72562800-7acf-11eb-952a-267337e4de09.png)

<br/>

# Machine Learning Concept

> Machine Learning(기계 학습)은 인공 지능의 한 분야로, 컴퓨터가 학습할 수 있도록하는 알고리즘과 기술을 개발하는 분야를 말한다. (Wikipedia)

- 주어진 데이터를 통해서 입력변수와 출력변수간의 관계를 만드는 함수 f를 만드는 것

<img src="https://user-images.githubusercontent.com/64063767/109463153-e4b31200-7aa7-11eb-8a1a-10f173066c6e.png" alt="image" style="zoom: 67%;" />

## ML Algorithms

![Machine Learning Algorithm(Regression)](https://user-images.githubusercontent.com/64063767/115368315-ed9ba680-a201-11eb-90c1-b51eb622fd88.png)

![Machine Learning Cheet Sheet](https://user-images.githubusercontent.com/64063767/115368309-eb394c80-a201-11eb-918e-a3d3d51575c2.png)

<br/>

## 1. 지도 학습(Supervised Learning)

- **학습 데이터마다 레이블(정답)을 가지고 있음**

- 출력변수 Y와 입력변수 X 사이의 관계에 대해 모델링을 하는 것

<img src="https://user-images.githubusercontent.com/64063767/109464434-001f1c80-7aaa-11eb-90cc-96983be3d95e.png" alt="image" style="zoom: 67%;" />

### 1.1 회귀(Regression)

- 출력변수 Y가 연속형(Continuous)인 경우에 회귀 모델링

- 최적의 회귀 모델을 만든다는 것은 전체 데이터의 잔차의 합이 최소가 되는 모델을 만드는 것

### 1.2 분류(Classification)

- 출력변수가 이산형(Discrete)인 경우에 분류 모델링

<br/>

## 2. 비지도 학습(Unsupervised Learning)

- **학습 데이터에 레이블(정답)이 없음**

- 입력만 있고 출력은 없는 상태에서 이루어지는 학습

- 데이터에 내재되어있는 고유의 특징을 탐색

### 2.1 군집(Clustering)

- **유사한 데이터끼리 그룹화**

![image](https://user-images.githubusercontent.com/64063767/152634326-44f44cef-8fdb-4905-8d03-6e9758128c2c.png)

### 2.2 주성분분석(PCA)

- **독립변수들의 차원을 축소화**

![image](https://user-images.githubusercontent.com/64063767/152634714-da857ca8-3d63-4089-815f-5466c4887d92.png)

<br/>

## 3. 강화 학습(Reinforcement Learning)

- 최종 출력(정답)이 바로 주어지지 않고, 시간이 지나서 주어지는 경우에 적합한 학습 알고리즘

- Ex) 바둑: 승/패의 결과가 바둑기사의 한수에 주어지지 않고, 시간이 지난 후에 주어짐. 바둑기사는 매 순간 바둑판의 상황을 읽고 어떤 수를 두어야할지 고민한다.

- 어떤 Action이 최종 출력에 영향을 주었는지 불명확한 문제에 사용된다.

- 매 순간 어떤 Action을 선택할지 판단하고, 상황(state)에 대한 평가가 이루어져야 한다.

### Q-learning

- 수 많은 시뮬레이션을 통해 현재의 성택이 먼 미래에 보상이 최대가 되도록 학습 (ex. AlphaGo)

- Agent가 action을 취하고 환경에서 보상을 받고 이 보상이 최대가 되도록 최적의 action을 취하는 방법을 학습

<img src="https://user-images.githubusercontent.com/64063767/109465314-5476cc00-7aab-11eb-9205-1b011d6f9302.png" alt="image" style="zoom: 67%;" />