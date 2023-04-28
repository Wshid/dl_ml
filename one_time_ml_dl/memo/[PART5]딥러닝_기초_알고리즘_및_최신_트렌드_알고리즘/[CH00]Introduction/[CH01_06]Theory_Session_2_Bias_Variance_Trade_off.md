## CH01_06. [Theory Session 2] Bias Variance Trade-off

### 점 추정(point estimator)
- 정의
  - 표본으로부터 모수에 값에 가까우리라 예상되는 하나의 값을 제시하는 어떤 함수
  - i.e. 평균
    - $\hat{\theta_n} = f(x1,...,x_n), where x_i \in \theta$(i.i.d.; independently identically distributed)
      - 독립적이고 동일하게 분포된

### 함수 추정(function estimator)
- input과 output$(x,y)$의 관계에 대한 추정 -> 함수 추정
- 만약 $x,y$를 투영하는 함수 $f$가 있다면, 아래와 같음
  - $y = f(x) + \epsilon$
  - 이 때, $\epsilon$은 $x$로부터 추론 불가한 에러
  - noise 같은 에러는 필연적으로 존재

### 추정 값의 편향(bias)
- 모델의 예측 값들의 평균과
- 이상적인 모델의 예측값(혹은 실제 값의 평균)과의 차이
- $h(x)$를 모델, $f(x)$를 실제 이상적인 예측 함수라고 하면,
  - $Bias[h(x)] = E[h(x)] - f(x)$

### 추정 값의 분산(variance)
- 모델의 예측 값과 모델의 예측 값들의 평균 사이의 차이
  - $Var[h(x)] = E[(h(x) - E[h(x)])^2]$
  - 표준편차의 제곱

### 노이즈(noise)
- 실제 값과 이상적인 모델간의 차이(줄일 수 없는 에러)
  - $Noise[h(x)] = E[(y-f(x))^2] = E[\epsilon^2] = \sigma^2$

### 분산과 편향과의 관계
- ![image](https://user-images.githubusercontent.com/10006290/234856788-b2b9690a-3378-4a73-99eb-87500b0b6fac.png)


### 편향 - 분산 트레이드 오프(Bias-Variance Tradeoff)
- 모델의 error란?
  - 실제 값 y와 모델의 예측 값$h(x)$의 차이
  - $E[(y-h(x))^2]$
- 제곱의 평균 = 분산과 평균의 제곱의 합과 같음
  - $Var(x) = E[x^2] - E[x]^2$
  - $E[(h(x)-E[h(x)])^2] + (E[h(x)] - f(x))^2 + E[(y-f(x))^2]$
    - Variance + Bias^2 + Noise
- 결국 모델의 복잡도에 따라 다음과 같은 관계를 가짐
  - ![image](https://user-images.githubusercontent.com/10006290/234858030-3fb4a824-b92f-4664-bf92-dd14eb0c75ac.png)
