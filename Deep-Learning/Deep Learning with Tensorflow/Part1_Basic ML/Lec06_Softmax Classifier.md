# Softmax Classifier

## 1. Multinomial Classification(다항 분류)

**Multinomial Classification을 Binary Classification을 활용하여 해결할 수 있다.**

<img src="https://user-images.githubusercontent.com/64063767/117544991-ceed3a80-b05e-11eb-8e50-2b37856fc5b4.png" alt="image" style="zoom:50%;" />

| ![image](https://user-images.githubusercontent.com/64063767/117546097-b2073600-b063-11eb-83fb-d8d1254943b9.png) | ![image](https://user-images.githubusercontent.com/64063767/117546081-9bf97580-b063-11eb-8352-8ca7b4b6cae1.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

<br/>

## 2. Softmax function

**Softmax function**

- **입력받은 값을 0 ~ 1사이의 정규화된 값으로, 즉 확률로 출력해주는 함수**
- **각각의 Softmax function 출력값의 합은 1**

<img src="https://user-images.githubusercontent.com/64063767/117558150-9593e980-b0b5-11eb-9a93-f0430b779cbb.png" alt="image" style="zoom:50%;" />

<br/>

## 3. Cost function

**Cross-Entropy cost function**

- target과 hypothesis 값만이 loss에 영향을 미친다. 나머지는 one-hot encoding되기 때문에 0이 되고, softmax 함수를 거쳐나온 출력값(확률)이 1이면 loss는 0으로 가장 작고 그외에는 0~1 사이의 -log값이기 때문에 매우큰 loss를 가지게 되는것이다.

- 분류 class의 label만 1로 만들고 나머지는 0으로 만들기 때문에 y는 class 개수만큼의 차원을 가져야 한다.

| ![image](https://user-images.githubusercontent.com/64063767/117558840-7d26cd80-b0bb-11eb-871d-56e2d9a1252b.png) | ![image](https://user-images.githubusercontent.com/64063767/117559031-bd3a8000-b0bc-11eb-854c-d51dce0ea1b9.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

