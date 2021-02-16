## Train set / Validation set / Test set

https://ganghee-lee.tistory.com/38

https://3months.tistory.com/118

> 3등분으로 나누는 비율은 대체적으로 6:2:2를 가장 많이 쓰고, 이렇게 나누는 방법을 Simple Validation이라고 한다. Simple Validation 외에 k-Fold Validation이나 Leave-One-Out Validation 방법도 있지만 여기서는 Simple Validation 방법을 다룬다.

<br/>

- **Train set**

  분석 모델을 만들기위한 학습용 데이터

  **"모델을 학습하는데에는 오직 유일하게 Train set만 이용한다"**

  보통 Train set을 이용해 각기 다른 모델을 서로 다른 epoch로 학습을 시킨다.

  여기서 각기 다른 모델이란 hidden layer 혹은 hyper parameter에 약간씩 변화를 준 모델들이다.

<br/>

- **Validation set**

  여러 분석 모델 중 어떤 모델이 적합한지 선택하기 위한 검증용 데이터

  학습이 이미 완료된 모델을 검증하기 위한 dataset

  **"모델의 성능을 평가하기 위해서"**

<br/>

- **Test set**

  최종적으로 선택된 분석 모델이 얼마나 잘 작동하는지 확인하기 위한 결과용 데이터

<br/>

validation set을 사용하는 이유는 간단하다. 바로 "모델의 성능을 평가하기 위해서" 이다.  training을 한 후에 만들어진 모형이 잘 예측을 하는지 그 성능을 평가하기 위해서 사용한다. training set의 일부를 모델의 성능을 평가하기 위해서 희생하는 것이다. 하지만 이 희생을 감수하지 못할만큼 data set의 크기가 작다면 cross-validation이라는 방법을 쓰기도 한다. cross-validation은 training set을 k-fold 방식을 통해 쪼개서 모든 데이터를 training과 validation 과정에 사용할 수 있게 한다.

<br/>

**그러면 모델의 성능을 평가하면 뭐가 좋을까?** 

<br/>

첫 번째는 test accuracy를 가늠해볼 수 있다는 것이다. machine learning의 목적은 결국 unseen data 즉, test data에 대해 좋은 성능을 내는 것이다. 그러므로 모델을 만든 후 이 모델이 unseen data에 대해 얼마나 잘 동작할지에 대해서 반드시 확인이 필요하다. 하지만 training data를 사용해 성능을 평가하면 안되기 때문에 따로 validation set을 만들어 정확도를 측정하는 것이다. 두 번째는 모델을 튜닝하여 모델의 성능을 높일 수 있다. 예를 들어 overfitting 등을 막을 수 있다. 예를 들어 training accuracy는 높은데 validation accuracy는 낮다면 데이터가 training set에 overfitting이 일어났을 가능성을 생각해볼 수 있다. 그렇다면 overfitting을 막아서 training accuracy를 희생하더라도 validation accuracy와 training accuracy를 비슷하게 맞춰줄 필요가 있다. 예를 들어 Deep learing을 모델을 구축한다면 regularization 과정을 한다거나 epoch을 줄이는 등의 방식으로 overfitting을 막을 수 있다. 



즉, validation set은 training 과정에 관여를 하며, training이 된 여러가지 모델 중 가장 좋은 하나의 모델을 고르기 위한 셋이다. test set은 모든 training 과정이 완료된 후에 최종적으로 모델의 성능을 평가하기 위한 셋이다. 만약 test set이 모델을 개선하는데 쓰인다면, 그건 test set이 아니라 validation set이다. 만약 여러 모델을 성능 평가하여 그 중에서 가장 좋은 모델을 선택하고 싶지 않은 경우에는 validation set을 만들지 않아도 된다. 하지만 이 경우에는문제가 생길 수 있다. (test accuracy를 예측할 수도 없고, 모델 튜닝을 통해 overfitting을 방지할 수도 없다.)

<hr>

Validation set과 Test set의 공통점은 이 데이터를 통해 모델을 update 즉, **학습을 시키지 않는다**는 것이다.

<br/>

**"그렇다면 둘의 차이는 무엇일까?"**

<br/>

둘의 차이는 Validation set은 모델을 update, 즉 **학습을 시키진 않지만 학습에 '관여'**는 한다.

Test set은 **학습에 전혀 관여하지 않고 오직 '최종 성능'을 평가**하기 위해 쓰인다.

![image](https://user-images.githubusercontent.com/64063767/108048067-f1883c80-7089-11eb-9fdf-d235a3841647.png)



그림에서 우측으로 갈수록 epoch을 늘려가면서 train set을 학습시키는 과정이다. 가운데 그림은 train set 뿐만 아니라 unseen data에 대해서도 좋은 성능을 보일 것으로 보인다. 그러나 가장 우측그림을 보면 train set에 overfitting되어 다른 unseen data에 대해 안좋은 성능을 보일 것이다. 즉, train set으로 학습을 할 때 너무 높은 epoch로 학습시키면 overfitting의 문제가 있다.

![image](https://user-images.githubusercontent.com/64063767/108048542-825f1800-708a-11eb-86f5-30b9012a7a9d.png)

파란색 baseline을 기준으로 더 학습시키면 overfitting되어 test set에 대한 결과가 점점 안좋아진다. 떠라서 파란색 baseline까지만 학습을 해야한다. 다시말해, 파란색 baseline에 해당하는 epoch를 찾아야한다. 그러나 이때 test set은 '최종 성능' 평가할 때만 사용하므로 학습에 이처럼 관여해서는 안된다. 결국 여기서 validation set이 사용되는 것이다. 

<br/>

validation set을 사용하여 train set에 대한 epoch를 바꿔가면서 위 그림과 같은 error 곡선을 그린다.

그 후 baseline에 해당하는 epoch를 찾으면 해당 epoch까지만 모델을 학습시켜 test set으로 '최종 성능'을 평가한다. 한마디로 위 그림에서의 test error를 validation set에 의한 validation error라고 생각하면 된다.

<br/>

이렇게 validation set은 train set에 의한 epoch뿐만 아니라 다른 hyper parameter, hidden layer를 조정할때도 사용될 수 있다. 예를 들어, learning rate와 hidden layer를 조금 변형해가면서 validation set에 대한 accuracy를 보면서 적절한 hyper parameter, hidden layer를 결정하는 것이다.

<br/>

Validation set에 대한 accuracy가 중요한 이유는 학습에서

**1) overfitting에 빠지지 않고**

**2) unseen data에 대한 좋은 성능**

이 두가지가 핵심적이기 때문이다.

<br/>

따라서 최종 성능 평가를 위한 test 이전에 validation으로 어떤 모델을 어떤 epoch로 학습시킬때

unseen data에 대해서 좋은 성능을 보이는 모델이 무엇인지 파악하야 한다.