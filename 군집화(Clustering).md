# 군집화(Clustering)

> 대표적인 비지도 학습 알고리즘으로 정답 데이터 없이 데이터 속성들로만 데이터를 분류하는 알고리즘

![image](https://user-images.githubusercontent.com/64063767/152688182-75d7c31b-1f49-46e3-99d0-9a17f5ad38c8.png)

<br/>

## 1. 군집 알고리즘

- **비계층적 군집화(Partitioning Clustering)**: 사전에 군집의 수를 정해주는 군집화 방법

  - **중심점 기반 군집**: K-Means

  - **밀도 기반 군집**: DBSCAN

- **계층적 군집화(Hierarchical Calustering)**: 각 개체가 독립적인 각각의 군집에서 점차 거리가 가까운 대상과 군집을 이루는 군집화 방법

### 1.1 K-Means Clustering

> **군집 중심점(Centroid)** 기반 클러스터링

![K-Means Clustering](https://user-images.githubusercontent.com/64063767/152670471-48624d16-4dac-4324-8b70-a18cabb4842e.png)

#### K-Means Model Primary Parameter
- `n_cluters`: 군집 개수
- `init`: 초기 중심점 위치가 무작위로 지정되어 중심점 이동 iteration이 크게 증가하지 않도록 방지해주는 parameter
- `max_iter=300`: 중심점 이동 최대 횟수

#### 장점

- 일반적인 군집화에서 가장 많이 활용되는 알고리즘
- 알고리즘이 쉽고 간결하다.
- 대용량 데이터에도 활용이 가능하다.

#### 단점

- 거리 기반 알고리즘으로 속성(변수)의 개수가 많을 경우 군집화 정확도가 떨어진다.
  (PCA 차원축소를 적용해야할 수 있다)
- 반복을 수행할 때 반복 횟수가 많을 경우 수행 시간이 느려진다.
- **이상치(Outlier) 데이터에 취약**하다.

<br/>

### 1.2 Mean Shift Clustering

> KDE(Kernel Density Estimation)를 이용하여 **데이터 포인트들이 데이터 분포가 높은 곳으로 이동하면서 군집화**하는 알고리즘
>
> Mean Shift는 데이터 분포도에 기반하여 **자동으로 군집화 개수를 정한다.**
>
> 오직 **Bandwidth의 크기에 따라 군집화**를 수행한다. (Bandwidth에 민감하다)
>
> Computer Vision(CV), Obejct Tracking 분야에서 많이 활용된다.

![image](https://user-images.githubusercontent.com/64063767/152675836-31ddb259-fe85-4c55-849e-aac16d6bd3b6.png)

| <img src="https://user-images.githubusercontent.com/64063767/152675663-8371aa6c-2c0e-4071-af92-6548b859b0d6.png" alt="image" style="zoom: 67%;" /> | <img src="https://user-images.githubusercontent.com/64063767/152675695-1026da6c-ba0b-48ba-8731-6e95f81baeb6.png" alt="image" style="zoom:67%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

#### 모수적(Parametric) 추정

데이터가 특정 데이터 분포(가우시안 분포 등)를 따른다는 가정하에 데이터 분포를 찾는 방법으로 Gaussian Mixture 등이 있다.

#### 비모수적(Non-Parametric) 추정

데이터가 특정 분포를 따르지 않는다는 가정하에서 밀도를 추정. 관측된 데이터만으로 확률 밀도를 찾는 방법으로서 대표적으로 KDE(Kernel Density Estimation)가 있음.

#### KDE(Kernel Density Estimation)

- KDE는 커널(Kernel) 함수를 통해 어떤 변수의 확률밀도 함수를 추정하는 방식이다.
- 관측된 데이터 각각에 커널 함수를 적용한 값을 모두 더한 뒤 데이터 개수로 나누어서 확률 밀도 함수를 추정한다.
- 작은 bandwidth h값은 좁고 spike한 KDE로 변동성이 큰 확률밀도 함수를 추정(Overfitting)
- 큰 bandwidth h값은 과도하게 smoothing된 KDE로 단순화된 확률밀도함수를 추정(Underfitting)
- Mean Shift는 bandwidth가 클수록 적은 수의 클러스터링 중심점을, bandwidth가 작을수록 많은 수의 클러스터링 중심점을 가지게 된다.

<br/>

### 1.3 Gaussian Mixture Model(GMM)

> GMM은 군집화를 적용하고자 하는 데이터가 여러개의 다른 가우시안 분포를 가지는 모델로 가정하고 군집화를 수행한다.

<img src="https://user-images.githubusercontent.com/64063767/152686213-194e7da9-2c89-45b2-9f76-0943fbc33dd0.png" alt="image" style="zoom: 67%;" />

<img src="https://user-images.githubusercontent.com/64063767/152683909-8af3fcef-9f9b-4402-a9a8-3f51dff802a5.png" alt="image" style="zoom: 67%;" />

- 1000개의 데이터 세트가 있다면 이를 구성하는 여러 개의 정규분포 곡선을 추출하고, 개별 데이터가 이 중 어떤 정규분포에 속하는지 결정하는 방식
- GMM 모수 추정은 개별 정규분포들의 평균과 분산, 그리고 데이터가 특정 정규분포에 해당할 확률을 추정한다.
  - Expectation
    - 개별 데이터 각각에 대해서 특정 정규분포에 소속될 확률을 구하고 가장 높은 확률을 가진 정규분포에 소속
    - 최초에는 데이터들을 임의로 특정 정규 분포로 소속
  - Maximization
    - 데이터들이 특정 정규분포로 소속되면 다시 해당 정규분포의 평균과 분산을 구함
    - 해당 데이터가 발견될 수 있는 가능도를 최대화(Maximum likelihood)할 수 있도록 평균과 분산(모수)를 구함

<br/>

### 1.4 DBSCAN

> **밀도 기반** 클러스터링

![image](https://user-images.githubusercontent.com/64063767/152686072-1da6a390-b4b8-4197-9bae-6f3879f88c9f.png)

- **특정 공간 내에 데이터 밀도 차이를 기반**한 알고리즘으로 복잡한 기하학적 분포도를 가진 데이터 세트에 대해서도 군집화를 잘 수행한다.

- DBSCAN 알고리즘이 데이터 밀도 차이를 자동으로 감지하여 군집을 생성하므로 **사용자가 군집 개수를 지정할 수 없다.**
- 데이터의 밀도가 자주 변하거나, 모든 데이터 밀도가 크게 변하지 않으면 군집화 성능이 떨어진다.
- 피처의 개수가 많으면 군집화 성능이 떨어진다.

#### DBSCAN Primary Parameter

- `eps`: 개별 데이터를 중심으로 입실론 반경을 가지는 원형의 영역
- `min_samples`: 개별 데이터의 입실론 주변 영역에 포함되는 타 데이터 개수

<br/>

## 2. 군집 평가

### 실루엣 분석

> 다른 군집과의 거리는 얼마나 멀리 떨어져 있고, 동일 군집 끼리의 데이터는 얼마나 서로 가까운지 평가

<img src="https://user-images.githubusercontent.com/64063767/152671284-e21e9185-a526-47e5-a10e-fd1c7d612001.png" alt="image" style="zoom: 67%;" />

- 실루엣 분석은 각 군집 간의 거리가 얼마나 효율적으로 분리돼 있는지를 분석한다.
- 실루엣 분석은 개별 데이터가 가지는 군집화 지표인 실루엣 계수(silhouettee coefficient)를 기반으로 한다.
- 개별 데이터가 가지는 실루엣 계수는 해당 데이터가 같은 군집 내의 데이터와 얼마나 가깝게 군집화 되어있는지, 다른 군집에 있는 데이터와는 얼마나 멀리 분리되어 있는지를 나타내는 지표이다.
- 전체 실루엣 계수 평균값이 높을수록(1에 가까울수록) 군집화가 잘되었다고 판단할 수 있지만, 절대적인 군집화 척도는 아니다.
- 전체 실루엣 계수의 평균값과 함께 **개별 군집의 평균값 편차가 크지 않아야** 한다. 즉, 개별 군집의 실루엣 계수 평균값이 전체 실루엣 계수의 평균값에서 크게 벗어나지 않는 것이 중요하다.

- 실루엣 분석은 대용량 데이터에 대해서 수행시간이 기하 급수적으로 증가한다.
- **실루엣 분석으로 적정 군집의 개수를 탐색할 수 있다.**

<br/>

## References

- 파이썬 머신러닝 완벽 가이드

- [Selecting the number of clusters with silhouette analysis on KMeans clustering](https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html)

  