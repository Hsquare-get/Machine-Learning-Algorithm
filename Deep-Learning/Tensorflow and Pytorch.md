# Tensorflow VS Pytorch

> Tensorflow와 Pytorch는 **딥러닝 프레임워크**로 사용목적과 분야에 따라 사용성이 다르다.
>
> [Pytorch vs Tensorflow 비교](https://data-newbie.tistory.com/425)
>
> [하나의 조직에서 TensorFlow와 PyTorch 동시 활용하기](https://jeongukjae.github.io/posts/pingpong-torch-to-tf-tf-to-torch/)

|           | Tensorflow                                                   | Pytorch                                                      |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 목적      | 제품 생산에 쓰이는 모델 개발(**Production**)                 | 연구(**Research**)                                           |
| 배포사    | Google(2015)                                                 | Facebook(2017)                                               |
| 호환 언어 | Python, C++, JavaScript, Java, Go                            | Python, C++                                                  |
| 특징      | 1. **Static Graph** 사용하기 때문에 코드를 실행하기 전에 그래프를 다 만들어놔야한다<br />(parallelism, dependency driving scheduling으로 더 빠르고 효율적으로 학습할 수 있다는 장점도 존재)<br />2. 인공지능 언어모델 BERT와 ELMo의 호환성이 높음<br />(NLP 분야에서 유리)<br />3. Tensorflow 2.0으로 업그레이드되며 코드 업그레이드가 필요<br />4. 디버깅이 까다롭다<br />5. 업데이트로 많은 변경이 있어 매번 적응하고 새로 배우기 번거롭다<br />(layers ->slim -> estimators ->tf.kreas) | 1. **Dynamic Graph** 사용으로 실시간으로 데이터를 바꿔 넣어보며 비교가 가능하다<br />2. 효율적인 계산<br />3. 낮은 CPU 활용<br />4. numpy와 유사하고 파이썬 환경 시스템과 쉽게 통합할 수 있다<br />5. 직관적인 인터페이스<br /><br />(RNN, CNN, GAN 연구에 유리)<br /> |
| 커뮤니티  | 비교적 큼                                                    | 비교적 작음                                                  |
| 난이도    | 비교적 어려움                                                | 비교적 쉬움                                                  |

<br/>

## Distributed Training

| Tensorflow                                                   | Pytorch                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 분산 학습을 하려면 specific device에서 실행되도록 <br />모든 작업을 수동으로 코딩하고 fine tuning(미세 조정)해야 한다. | PyTorch는 Python의 비동기 실행에 대한 기본 지원을 활용하여 최적화한다. |

<br/>

## Visualization

| Tensorflow  | Pytorch     |
| ----------- | ----------- |
| TensorBoard | TensorBoard |

- Loss & Accuracy 같은 metrics를 추적하고 시각화하는 기능
- Computational Graph(ops and layers) 시각화하는 기능
- 시간이 지나면서 변화하는 weight(가중치), bias(편향), 또는 기타 tensor들의 히스토그램을 볼 수 있다.
- Displaying images, text, and audio data
- Profiling Tensorflow programs

<br/>

## Production Deployment

| Tensorflow                                   | Pytorch                                                      |
| -------------------------------------------- | ------------------------------------------------------------ |
| TensorFlow serving using **REST Client API** | Not exists framework to deploy models directly on the web<br/>But can use **Flask** or **Django** to deploy |

<br/>