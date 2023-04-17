## CH01_03. 선형회귀, 로지스틱회귀 그리고 log-likehood

### Classification
- 이산적(discrete)로 구성된 레이블을
  - 각각의 학습 데이터로부터 학습시키는 경우

### Regression
- **연속적인 레이블**을 각각의 학습 데이터로부터 학습시키는 경우
- 알파고의 경우에도
  - 기반은 강화학습이나
  - 가치 함수(value function)도 확률적으로 추론하기 위해 사용

### 선형 회귀로 이항 분류(binary classification) 진행
- Linear regression
  - $f(x) = \theta_1x + \theta_0$
- $f(x)$의 에러 제곱의 합(sum of squared residuals; RSS)을
  - 목적 함수로 최소화 하여, 최적의 함수를 찾음

$$
RSS = \sum_i^n(y_1 - \hat{y}_i)^2 = \sum_i^n(y_i - f(x_i)) = \sum_i^n(y_i - (\theta_0 + \theta_1x_i))^2
$$

- 위 값을 최소화
  - 이 최소값은 **미분한 값이 0이 될 떄를 의미**

### 로지스틱 회귀로 이항 분류 하기
- Linear Regression
  - $f(x) = \theta_1x + \theta_0$
- Logistic Regression
  - $f(x) = \frac{1}{1+e^{-x}}$
- Sigmoid 함수
  - 연속 함수이며, 대칭 함수(symmetric)이다
  - 미분이 쉽기 때문에, **gradient descent**에 적합
    - $f(x) - f(x)^2$

### 로지스틱 회귀: 로그 우도법(Loglihood)
- 이항 분류 -> 0, 1 예측
  - Bernoulli 분포를 따름(베르누이 분포)
  - 동전 던져서 앞면이 나오는 확률
    - $p=1/2$인 베르누이 분포
  - 주사위를 던져 3의 배수
    - $p=1/3$인 베르누이 분포
- 베르누이 분포
  - $Y ~ Ber(p), p = \sigma(\theta x)$
  - $P(Y = y | X = x) = \sigma(\theta x)^y * (1 - \sigma(\theta x))^{1-y}$
- 가능도(Likelihood): 모든 확률을 곱한 값
  - $L(\theta) = \prod_i P(Y = y^i | X = x^i) = \prod_i \sigma{\theta x_i}^{y_i} * (1 - \sigma({\theta x_i}))^{1-y_i}$
- **가능도**(우도)를 최대로 하는 최적의 $\theta$를 구하는 것이 목표

#### 가능도 단순화
- 로그 씌우기
  - $log a * b = log a + log b$를 활용하여 아래와 같이 단순화

$$
log(L(\theta)) = \sum_i [y_ilog(\sigma(\theta x_i)) + (1 - y_i) log(1 - \sigma({\theta x_i}))] 
$$

- 이 함수를 maximizing 하기 보다, 음수를 취해 줄이는 방향의 **손실 함수**(loss function)으로 되면
  - **negative log-likelihood**함수가 됨

$$
min_\theta J(\theta) = min_\theta(- \sum_i [y_ilog(\sigma(\theta x_i)) + (1 - y_i) log(1 - \sigma({\theta x_i}))])
$$
- 함수가 convex하기 때문에, Gradient Descent로 최적화 문제로 풀 수 있음
  - 이는 **Cross Entropy**와 같음
- convex하다
  - $y=x^2$과 같은 볼록함수