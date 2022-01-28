# 조기종료(Early Stopping)

**Early Stopping**은 신경망 학습 모델(Neural Network)이 과적합 되는 것을 방지하도록 만드는 정칙화(regularization) 기법 중 하나이다.

훈련 데이터(train set)와는 별도로 검증 데이터(validation set)를 준비하고, 매 epoch 마다 검증 데이터에 대한 오류(validation loss)를 측정하여 모델의 훈련 종료를 제어한다.

과적합이 발생하기 전까지 training loss와 validation loss 둘 다 감소하지만, 과적합이 일어나면 training loss는 감소하는 반면에 validation loss는 증가한다. 이 때 early stopping을 통해 validation loss가 증가하는 시점에 훈련을 멈추도록한다.

![image](https://user-images.githubusercontent.com/64063767/151492784-6c4b9fca-f426-4f93-bfa8-89509d3dad8d.png)

<br/>

## Early Stopping 예제

Keras에서는 사용자가 early stopping을 손쉽게 적용할 수 있도록 callbacks란 기능을 제공한다.

```python
callbacks = [keras.callbacks.EarlyStopping(monitor='val_loss', patience=5)]

# Training the model
model.fit(x_train, y_train,
          batch_size=32,
          epochs=100,
          validation_data=(x_valid, y_valid),
          callbacks=callbacks
         )
```

Keras의 EarlyStopping은 2개의 파라미터를 입력받는다.

monitor는 어떤 값을 기준으로 하여 훈련 종료를 결정할 것인지를 입력받고, patience는 기준되는 값이 연속으로 몇 번 이상 향상되지 않을 때 종료시킬 것인지를 나타낸다.

위의 코드에서는 validation loss를 기준으로 훈련을 제어한다. 이 때 validation loss가 이전 epoch의 validation loss보다 증가됐다고 하여 바로 중지하지 않고, patience 만큼 연속으로 validation loss가 낮아지지 않는 경우에 종료되도록 설정되었다.

patience는 모델이 아직 더 향상될 수 있지만, 우연히 validation loss가 낮게 나와서 훈련이 종료되버리는 상황을 피하기 위한 파라미터이다.

<br/>

## Early Stopping 주의사항

Keras의 EarlyStopping 메서드를 사용하면 조기종료를 구현하는 것은 쉽다. 하지만 patience가 0이 아닌 경우 주의해야할 사항이 있다.

만약 20번째 epoch까지는 validation loss가 감소하다가 21번째부터 계속해서 증가한다고 가정해보자. patience를 5로 설정했기 때문에 모델의 훈련은 25번째 epoch에서 종료된다.

그렇다면 훈련이 종료됐을 때 이 모델의 성능은 20번째와 25번째 모델 중 어느쪽 모델의 성능일까?

위 예제에서 적용된 early stopping은 훈련을 언제 종료시킬지를 결정할 뿐이고, 가장 좋은 성능을 갖는 모델을 저장하지는 않는다.

따라서 early stopping과 함께 모델을 저장하는 **callback 함수**를 반드시 활용해야만 한다.

```python
callbacks = [
    keras.callbacks.EarlyStopping(monitor='val_loss', patience=5),
    keras.callbacks.ModelCheckpoint(
        filepath='best_model.h5',
        monitor='val_loss',
        save_best_only=True)
]

# Training the model
keras_model.fit(x_train, y_train,
                batch_size=32,
                epochs=100,
                validation_data=(x_valid, y_valid),
                callbacks=callbacks)

# Load best model
keras_model_best = keras.models.load_model('best_model.h5')
```