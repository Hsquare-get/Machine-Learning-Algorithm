# 상관분석(Correlation Analysis)

- reference
  - [Correlation Analysis](https://m.blog.naver.com/PostView.nhn?blogId=libido1014&logNo=120115838312&proxyReferer=https:%2F%2Fwww.google.com%2F)
  - [정규성 검정(Normality Test)](https://m.blog.naver.com/y4769/221896138434)
  - [Python을 이용하여 단순 선형회귀 모델 적합해보기](https://zephyrus1111.tistory.com/52)
  - [선형회귀(Linear Regression) - Python Example Code](http://hleecaster.com/ml-linear-regression-example/)

<br/>

## 1. 상관 계수를 보는 방법

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
       - 

- 

<br/>

### 1.2 Spearman 상관계수(Spearman's Correlation Coefficient)

<br/>

## 2. 그래프를 통해 상관관계를 보는 방법

- scatter plot

  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  
  height = [65, 71, 69, 68, 67]
  weight = [112, 136, 153, 142, 144]
  
  X = df['height']
  Y = df['weight']
  plt.plot(X, Y)
  plt.show()
  ```

  ```python
  import pandas as pd
  import matplotlib.pyplot as plt
  import matplotlib
  matplotlib.rcParams['axes.unicode_minus'] = False ## 마이나스 '-' 표시 제대로 출력 
  from statsmodels.formula.api import ols
  
  fit = ols('Work_hours ~ Lot_size', data=df).fit()
  fit = ols('Work_hours ~ Lot_size - 1',data=df).fit() # 절편항 제거
  fit.summary() # 결정계수와 회귀계수추정값, 검정통계량, p-value 확인
  
  ## 회귀 계수
  print(fit.params.Intercept) ## 절편
  print(fit.params.Lot_size) ## 기울기
  
  ## 시각화
  fig = plt.figure(figsize=(8,8))
  fig.set_facecolor('white')
  
  plt.scatter(df['Lot_size'],df['Work_hours']) ## 원 데이터 산포도
  plt.plot(df['Lot_size'],fit.fittedvalues,color='red') ## 회귀직선 추가
  
  plt.xlabel('Lot Size', fontsize=15)
  plt.ylabel('Work Hours',fontsize=15)
  plt.show()
  ```

  

<br/>

## 3. 모델링 방법

### 3.1 단순 선형회귀(Simple Linear Regression)

$$
Y = aX + b
$$

- 종속변수 Y와 독립변수 X 데이터가 있을 때 단순 선형회귀 모델을 만들어 상관성 분석을 한다.

  ```python
  import statsmodels.api as sm
  # from statsmodels.formula.api import ols
  
  height = [65, 71, 69, 68, 67]
  weight = [112, 136, 153, 142, 144]
  
  model = sm.OLS(weight, height)
  print(fitted_model.summary())
  print(fitted_model.params) # 회귀 계수
  ```

  ```python
  from sklearn.linear_model import LinearRegression
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  
  # DataFrame
  Lot_size = [80, 30, 50, 90, 70]
  Work_hours = [399, 121, 221, 376, 361]
  
  ### sklearn linear regression ###
  x = df['Lot_size'].values.reshape(-1,1) # 차원 증가 시켜준다.
  y = df['Work_hours']
  
  fit = LinearRegression().fit(x,y)
  
  # 회귀 계수
  print(fit.intercept_) # 절편
  print(fit.coef_) # 기울기
  
  # 예측값
  print(fit.predict([[70]]))
  print(fit.predict(x))
  
  plt.plot(x, y, 'o')
  plt.plot(x, fit.predict(x))
  plt.show()
  ```

  

