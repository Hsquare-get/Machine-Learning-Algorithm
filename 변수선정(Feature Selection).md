# 변수선정(Feature Selection)

모델을 구성하는 주요 변수(feature)들을 선택해야 한다.

- 불필요한 다수의 변수들로 인해 모델 성능을 떨어뜨릴 가능성을 제거
- 설명 가능한 모델이 될 수 있도록 변수들을 선별
- 변수 선정 기준
  - 변수 데이터 분포
  - NULL 여부
  - 변수간 상관도
  - 타겟 데이터와의 상관도
  - feature importance 참고

<br/>

## Recursive Feature Elimination(RFE)

- 모델 최초 학습 후 변수 중요도 선정
- 변수 중요도가 낮은 속성들을 차례로 제거해가면서 반복적으로 학습/평가를 수행하여 최적 변수 추출
- 수행시간이 오래 걸리고, 낮은 속성들을 제거해 나가는 메커니즘이 정확한 feature selection을 찾는 목표에 정확히 부합하지 않을 수 있음 

- 실제로는 거의 사용되지 않는 feature selection 방식

<br/>

## Permutaion Importance

- 특정 변수들의 값을 완전히 변조했을 때 모델 성능이 얼마나 저하되는지를 기준으로 해당 변수의 중요도를 산정
- 학습 데이터를 제거하거나 변조하면 다시 재학습을 수행해야하므로 수행시간이 오래걸림

- 일반적으로 테스트 데이터(검증 데이터)에 특정 변수들을 반복적으로 변조한 뒤 해당 변수의 중요도를 평균적으로 산정

<br/>

## Feature Importance가 변수 선정의 절대적 기준이 될 수 없는 이유

Tree-based 알고리즘에서 정보이득이나 지니계수를 통해 노드 분기에서 중요한 역할을 할 뿐, 모델을 잘 설명하는 변수 선정의 절대적 기준이 될 수 없다. 따라서 feature importance가 낮은 하위 변수들을 제거하는 것이 아니라 변수별로 A/B test를 진행하면서 변수를 선정해야 한다.

- 최적 tree 구조를 만들기 위한 feature들의 impurity가 중요 기준임
- feature importance는 낮게 평가되었지만 실제로는 중요한 특성일 수 있기 때문에 특성을 제거하면 모델 성능이 저하될 수 있음
- 타겟 데이터와 관련이 없어도 feature importance가 높아질 수 있음
- feature importance는 학습 데이터를 기반으로 생성됨. 테스트 데이터에서는 달라질 수 있음
- feature importance는 number형의 높은 cardinality feature에 biased 되어 있음

![Feature importance](https://user-images.githubusercontent.com/64063767/152188269-84cde91d-4df7-4b76-a584-ebd5db706b17.png)

<br/>

## References

- [파이썬 머신러닝 완벽 가이드](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EC%99%84%EB%B2%BD%EA%B0%80%EC%9D%B4%EB%93%9C)