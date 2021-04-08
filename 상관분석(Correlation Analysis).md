# 상관분석(Correlation Analysis)

- reference
  - [Correlation Analysis](https://m.blog.naver.com/PostView.nhn?blogId=libido1014&logNo=120115838312&proxyReferer=https:%2F%2Fwww.google.com%2F)
  - [정규성 검정(Normality Test)](https://m.blog.naver.com/y4769/221896138434)
  - [Python을 이용하여 단순 선형회귀 모델 적합해보기](https://zephyrus1111.tistory.com/52)
  - [선형회귀(Linear Regression) - Python Example Code](http://hleecaster.com/ml-linear-regression-example/)

<br/>

## 1. 상관 계수로 상관성을 보는 방법

### 1.1 Pearson 상관계수(Pearson's Correalation Coefficient)

- Pearson 상관계수는 **두 연속형 변수 사이의 선형적인 상관성(linear correlation)**을 분석하는데 사용된다.

- 전제

  1. 두 변수는 모두 **연속형 변수**이어야 한다.
  2. 두 변수 중 적어도 한 변수는 **정규성**을 만족해야 한다.

  3. 위의 두가지 전제를 만족시키지 못할 경우 비모수적인 방법을 사용한다.

- 검정통계량과 가설검정

  1. 가설
     - **귀무가설(H0)**: 모집단에서 두 변수 사이에 선형적인 **상관성이 없다**.
     - **대립가설(H1)**: 모집단에서 두 변수 사이에 선형적인 **상관성이 있다**.
  2. Pearson의 상관계수(r) 계산

  <img src="https://user-images.githubusercontent.com/64063767/113267635-8c269d00-9311-11eb-9935-f3bc32297dac.png" alt="image" style="zoom: 67%;" />

  1. 검정통계량과 가설검정

     - Sample Size(n) < 150이면 검정통계량은 r이다. 이 r을 이미 알려진 확률 분포에서 검정한다.
     - N > 150이면 검정통계량은 (수식 정확한지 다시보기)

     $$
     t = \sqrt{(n-2) / (1-r^2)}
     $$

     - 이 t값을 자유도가 n-2인 t-분포에서 검정한다.
     - r이 클 수록 귀무가설이 기각될 확률, 즉 모집단에서 두 변수 사이에 선형적인 상관성이 있을 확률이 커진다.

  2. Pearson 상관계수(r) 해석

     - p-value가 0.05 유의수준보다 낮아 귀무가설이 기각되고 대립가설이 채택되었을 때, 즉 모집단에서 두 변수 사이에 선형적인 상관성이 있다는 것이 인정되었을 때 r을 해석하여 사용한다.
     - Pearson 상관계수(r) 특징
       - r은 두 변수 사이의 선형적인 **상관성의 정도**를 알려준다. 만일 상관분석을 시행한 후 변수들간에 상관성이 있다는 것이 인정된다면 회귀분석(Regression Analysis)을 시행한다.
       - **r을 가지고 비선형적인 상관성은 알 수 없으며, 또한 두 변수 사이의 인과성도 알 수 없다.**
       
         


<br/>

### 1.2 Spearman 상관계수(Spearman's Correlation Coefficient)

<br/>

## 2. 산점도를 통해 상관성을 보는 방법

```python
import matplotlib.pyplot as plt

# outdoor temp & indoor temp
x = df['outdoor_temp']
y = df['indoor_temp']
plt.scatter(x='outdoor_temp', y='indoor_temp', data=df)
```

<img src="https://user-images.githubusercontent.com/64063767/113974260-951aef80-9878-11eb-9ce4-a2ef3d6aa1bd.png" alt="image"  />

<br/>

## 3. 모델링을 통해 상관성을 보는 방법

### 3.1 단순 선형회귀(Simple Linear Regression)

> 종속변수 Y와 독립변수 X 데이터가 있을 때 단순 선형회귀 모델을 만들어 상관성 분석

$$
Y = \beta_0 + \beta_1X + \epsilon
$$

#### 3.1.1 통계표로 모델 검정

```python
import statsmodels.api as sm

# 통계적인 방법
# statsmodel = sm.OLS(y, x).fit() # 절편 미포함
statsmodel = sm.OLS.from_formula("S1_humi ~ humidity", humi_inout).fit()

display(statsmodel.summary())
print(statsmodel.params)
```

![image](https://user-images.githubusercontent.com/64063767/113971470-cc3ad200-9873-11eb-8c50-4c5fd5837575.png)

<br/>

#### 3.1.2 sklearn 선형회귀 모델링

```python
from sklearn.linear_model import LinearRegression

# 단순선형회귀(Simple Linear Regression) 모델링
x = humi_inout['humidity'].values.reshape(-1,1)
y = humi_inout['S1_humi'].values.reshape(-1,1)
slrm = LinearRegression().fit(x, y)

print('y절편:', slrm.intercept_)
print('회귀계수(기울기):', slrm.coef_)

# 예측값
predicted = slrm.predict(x)

plt.plot(x, y, 'o')
plt.plot(x, slrm.predict(x))
plt.show()
```

![image](https://user-images.githubusercontent.com/64063767/113971698-3fdcdf00-9874-11eb-9627-5ad93e078d47.png)

