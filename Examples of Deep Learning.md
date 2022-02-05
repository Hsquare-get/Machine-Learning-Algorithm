# Deep Learning

## 1. Artificial Neural Network(ANN)

### Multi-Layer Perceptron(MLP)

인공신경망(ANN)에서 은닉층이 2개 이상인 신경망을 Multi-Layer Percetptron이라고 한다.

<img src="https://user-images.githubusercontent.com/64063767/109469988-25178d80-7ab2-11eb-90bb-3a5f60717b07.png" alt="image" style="zoom:67%;" />

- 입력(Input layer), 은닉(Hidden layer), 출력(Output layer)층으로 구성된 모형으로서 각 층을 연결하는 노드의 가중치(weight)를 업데이트하면서 학습
- 다층의 layer를 통해 복잡한 데이터의 학습이 가능하도록 함(graphical representation learning)
- 알고리즘 및 GPU의 발전이 deep learning의 부흥을 이끌었다.
- Overfitting이 심하게 일어나고 학습시간이 매우 오래걸린다.

<br/>

## 2. CNN(Convolutional Neural Network)

- 이미지 처리에 사용되는 Deep Learning

- 이미지의 지역별 feature를 뽑아서 Neural Network 학습
- Object detection, Image Resolution, Style transfer, Colorization

<img src="https://user-images.githubusercontent.com/64063767/109478467-a1af6980-7abc-11eb-95b6-69401eae173f.png" alt="image" style="zoom:67%;" />

<br/>

## 3. RNN(Recurrent Neural Network)

- 기존 Neural Network(Vanila NN)로는 Sequence data를 처리할 수 없었기 때문에 새로운 Neural Network 모델을 만든 것이 RNN(Recurrenc Neural Network)이다.

- 데이터의 순서에 따라 의미가 달라지고 순서에 종속적인 시퀀스 데이터를 처리하는 시퀀스(Sequence) 모델이다.
- Hidden Node가 방향성을 갖는 엣지로 연결되어 순환구조를 이루는 인공신경망이다.
- 시간 변화적 특징을 가지는 벡터모델링에 적합한 구조

<img src="https://user-images.githubusercontent.com/64063767/109481447-16d06e00-7ac0-11eb-835e-8719aeb14b93.png" alt="image" style="zoom:67%;" />

<br/>

## 4. AutoEncoder

- X를 가지고 X를 예측한 다음에 내부에서 패턴을 찾아내는 Unsupervised Learning
- 기존의 Neural Network 형태에서 출력값과 입력값의 개수가 같은 모델
- 좌우 대칭으로 하는 입출력층으로 구성되어 원본 데이터를 encoder를 통해 압축한 뒤 다시 decoder를 통해 복구하는 작업으로 특징을 추출하여 학습한다.
- 특성
  1. AutoEncoder는 data-specific해서 이제껏 훈련된 데이터와 비슷한 데이터로만 압축될 수 있다.
  2. AutoEncoder는 손실이 있다. 압축 해제된 결과물은 원본보다 좋지 않다. 따라서 손실없는 산술압축과는 다르다.
  3. 예제 데이터로부터 자동적으로 학습하는데 유용하다. 특정 종류의 입력값에 대해 잘 작동하는 특별한 형태의 알고리즘을 쉽게 훈련시킬 수 있다.

<img src="https://user-images.githubusercontent.com/64063767/109482216-11bfee80-7ac1-11eb-8f6f-16e62ad54276.png" alt="image" style="zoom: 67%;" /> <img src="https://user-images.githubusercontent.com/64063767/109482757-bfcb9880-7ac1-11eb-84bc-6b98e32a6741.png" alt="image" style="zoom: 67%;" />

<br/>

## 5. GAN(Generative Adversarial Network)

- Data를 만들어내는 **Generator**와 만들어진 data를 평가하는 **Discriminator**가 서로 대립적(Adversarial)으로 학습해가며 성능을 점차 개선해나간다.

- x: real data, z: noise data, G(z): fake data

  - Discriminator를 학습시킬 때에는 D(x)가 1이 되고 D(G(z))가 0이 되도록 학습시킴

    (진짜 데이터를 진짜로 판별하고, 가짜 데이터를 가짜로 판별할 수 있도록)

  - Generator를 학습시킬 때에는 D(G(z))가 1이 되도록 학습시킴

    (가짜 데이터를 discriminator가 구분 못하도록 학습, discriminator를 헷갈리게 하도록)

- 실제하지 않는 이미지(BigGAN), 그림을 실사 이미지로 또는 실사 이미지를 그림 이미지로(CycleGAN)
- SOTA(State-of-the-art) Model: 가장 최신식의 모델이라는 뜻(현재 SOTA 모델은 BigGAN이 아님)

<img src="https://user-images.githubusercontent.com/64063767/109485844-7b41fc00-7ac5-11eb-9754-991cdd2345ab.png" alt="image" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/64063767/109486279-01f6d900-7ac6-11eb-97b6-5c5c73bc6c26.png" alt="image" style="zoom:67%;" />

