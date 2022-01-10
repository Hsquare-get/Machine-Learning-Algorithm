# Basic Concept of Deep Learning

## 1. Neuron

> 뉴런은 생물체의 신경계를 이루는 신경세포이다. 
>
> Artificial Neural Network(ANN)은 이 신경 세포 뉴런을 추상화한 Artificial Neuron으로 구성된 네트워크이다.

![image](https://user-images.githubusercontent.com/64063767/148792729-0b9404ef-0f0e-4ef1-a915-b9678c2d1de5.png)

<br/>

## 2. Activation function

> 활성화 함수는 입력신호(input)와 가중치(weight), 그리고 편향(bias)까지 신호의 총 합을 다음 뉴런으로 전달 여부를 결정하는 함수이다.

![image](https://user-images.githubusercontent.com/64063767/148792175-2c326867-9442-49a4-93ee-fbb42f64a2ba.png)

<br/>

## 3. Logic Gate

![image](https://user-images.githubusercontent.com/64063767/148809077-4bae0244-8dbc-4ead-9494-59c755e0f41b.png)

> 각 논리게이트 OR, AND, NAND 진리표에서 퍼셉트론 구조는 모두 동일하며 다른 것은 매개변수(w,b)뿐이다.
>
> 따라서 매개변수의 값만 적절히 조정하면 OR, AND, NAND 모두 구현할 수 있다.

```python
import numpy as np

# OR Gate
def OR(x1,x2):
    x = np.array([x1,x2])
    w = np.array([0.5,0.5])
    b = -0.2
    signal_sum = np.sum(w*x) + b
    if sinal_sum <= 0:
        return 0
    else:
        return 1

# AND Gate
def AND(x1,x2):
    x = np.array([x1,x2])
    w = np.array([0.5,0.5])
    b = -0.7
    signal_sum = np.sum(w*x) + b
    if sinal_sum <= 0:
        return 0
    else:
        return 1

# NAND Gate
def NAND(x1,x2):
    x = np.array([x1,x2])
    w = np.array([0.5,0.5])
    b = 0.7
    signal_sum = np.sum(w*x) + b
    if sinal_sum <= 0:
        return 0
    else:
        return 1
```

<br/>

## 4. Perceptron

### XOR Problem

>단층 퍼셉트론으로 OR, AND, NAND 게이트는 구현가능하지만 XOR 게이트는 구현할 수 없다. 
>
>선형적으로 정확하게 구분할 수 없다.

![image](https://user-images.githubusercontent.com/64063767/148796320-fad1bda0-5917-49db-b214-79d81a5276ef.png)

> 이 문제를 해결하기 위해 MIT AI Lab Marvin Minsky 교수가 다층 퍼셉트론(MLP) 개념을 도입.
>
> 하지만 초기에는 weight와 bias를 조정할 수 없었다.

| Logic Gate                                                   | Truth Table                                                  | Multi-Layer Perceptron                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image](https://user-images.githubusercontent.com/64063767/148807389-efe7fe54-f273-475e-968c-16a4018289e1.png) | ![image](https://user-images.githubusercontent.com/64063767/148807512-33732301-5ee4-4c53-8f35-5bc7e41632e8.png) | ![image](https://user-images.githubusercontent.com/64063767/148800948-caaed52b-3a60-4c4a-b474-e0d5f6cfd587.png) |

```python
# XOR Gate
def XOR(x1,x2):
    s1 = NAND(x1,x2)
    s2 = OR(x1,x2)
    y = AND(s1,s2)
    return y
```

<br/>

## 5. Backpropagation

> 오차역전파 알고리즘을 통해 weight와 bias를 조정할 수 있었다.

![Backpropagation](https://machinelearningknowledge.ai/wp-content/uploads/2019/10/Backpropagation.gif)

<br/>

## 6. Vanishing & Exploding Gradient Problem

> 오차역전파 알고리즘은 출력층에서 입력층으로 오차 그래디언트를 흘려보내면서 각 뉴런의 입력값에 대한 손실함수의 그래디언트를 계산한다. 이렇게 계산된 그래디언트를 경사하강법(Gradient Descent) 단계에서 각 가중치를 업데이트 한다.
>
> 하지만 은닉층이 많은 심층신경망에서는 역전파 알고리즘이 입력층으로 전달됨에 따라 그래디언트가 점점 작아져 결국 가중치가 업데이트되지 않고 학습이 되지 않는 **Vanishing Gradient** 문제가 발생한다.
>
> 반대로, 역전파 과정에서 그래디언트가 점점 커져 입력층으로 갈수록 가중치가 기하급수적으로 커지게되는 문제를 **Exploding Gradient**이라고 한다.

![image](https://user-images.githubusercontent.com/64063767/148804128-83ac2ae0-6a3d-448d-82b3-0b6483d793ea.png)
