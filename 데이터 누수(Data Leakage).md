# 데이터 누수(Data Leakage)

- Reference

  - [Data Leakage-Rafael Pierre](https://mlopshowto.com/data-leakage-part-i-think-you-have-a-great-machine-learning-model-think-again-ad44921fbf34)
  - [Data Leakage-Kaggle](https://www.kaggle.com/alexisbcook/data-leakage)
  - [Data Leakage-DACON](https://dacon.io/competitions/official/235720/support/403125?page=1&dtype=recent)

<br/>

## What is data leakage?

- **data leakage는 training data 이외의 밖에서 유입된 정보가 모델을 만드는데 사용될 때 발생**한다. 이러한 추가적인 정보를 통해 모델은 다른 방법으로는 알지 못하는 무언가를 배우거나 알 수 있으며, 생성되는 모델의 예상 성능을 무효화할 수 있다. 결론적으로 data leakage로 인해 엉뚱한 모델이 만들어지고, 해석이 무의미해질 수 있다.

- data leakage로 인해 완전히 잘못된 예측 모델이 만들어지거나 지나치게 낙관적인 결과, 즉 과적합 문제를 일으킬 수 있다.
- 예를들어, 모델을 사용하여 예측을 수행하려는 시점에 실제 값을 실제로 사용할 수 없는 경우 데이터 누수가 발생할 수 있다.
- **모델 학습을 위해 사용하는 데이터가 예측하려고하는 정보를 가지고 있을 때** 누수가 발생한다.

<br/>

## Data Leakage Types

1. 타겟 누수(Target Leakage)
   - 타겟 누수는 예측 시점에서 사용할 수 없는 데이터가 데이터 셋에 포함되어 있을 때 발생한다.
   - 이런 유형의 데이터 누수를 방지하려면, 타겟 값이 결정된 후 생성된 모든 변수들을 데이터셋에서 제외해야 한다.
2. 훈련-테스트 오염(Train-Test Contamination)
   - 훈련 데이터와 검증 데이터를 제대로 구분하지 않았을 때 발생한다.
   - train_test_split() 함수를 호출하기 전 전처리를 실행하게 되면 모델의 검증 점수가 높으므로 신뢰도가 높지만, 실제로 배포할 때에는 성능이 저하된다.
   - 만약, 검증 데이터가 train_test_split() 함수로 생성됐다면 검증 데이터를 모든 fitting에서 제외하고, 전처리 단계의 fitting에 포함시켜야 한다. 이는 scikit-learn의 pipeline을 이용하면 된다. 교차 검증을 사용할 때는 파이프 라인 내에서 전처리를 수행하는 것이 훨씬 중요하다. 

<br/>

## What is the problem?

- data leakage는 아래와 같은 복잡한 데이터에서 더욱 문제점을 가진다.
  - 시계열 데이터의 경우 훈련세트와 테스트세트로 나누는 것이 어렵다.
  - 무작위 샘플링 방법을 구축하기 어려울 수 있는 그래프 문제
  - 샘플은 크기와 타임스탬프가 있는 별도의 파일에 저장되는 사운드 및 이미지와 같은 아날로그 관측

<br/>

## How to minimize the data leakage?

1. cross validation folds 내에서 데이터 준비를 수행한다.
   - 데이터에 대해 정규화(Normalization) 또는 표준화(Standardization)를 한 후, cross validation을 이용해 모델의 정확도를 측정하면 data leakage가 발생한다.
   - python의 scikit-learn의 pipeline을 활용하면 scaling같은 전처리 과정을 훈련세트와 테스트세트에 각각 한번에 진행시킬 수 있다.

2. 개발된 모델의 최종 온전성 검사를 위해 validation 데이터셋을 따로 보유한다.
   - training data를 train set과 validation set으로 나누고 validation set을 따로 보유하는 것 
3. 일시적 제거: 관찰이 일어난 시간보다 사실이나 관찰에 대해 배운 시간에 초점을 맞추어 관심 이벤트 직전의 모든 데이터를 제거한다.
4. 소음 추가: 입력 데이터에 임의의 노이즈를 추가하여 누출 가능성이 있는 변수의 영향을 부드럽게 한다.
5. 누출 변수 제거

