## CH01_05. [Theory Session 1] 경험적 위험도와 일반화

### 일반화 에러(generalization error), 실제 위험도(true risk)
- 일반적인 지도학습에서
  - 음수가 아닌 실수(real-value)인 손실함수(loss)를
  - 머신러닝 모델 f에 대해 나타낸다면
    - $L(f(x), y) = L(\hat{y}, y)$
- 새로운 데이터 $(x,y)$에 대해, ML 모델 $f$의 실제 위험도(true risk)를 아래와 같이 정의 가능
  - $R(f) = E[L(f(x)), y] =  \int L(f(x), y) \,dP(x,y)$
- 이 때, 이 값을 **일반화 에러**(generalization error)라고 함
- **딥러닝**을 포함한 머신러닝의 목표는
  - 일반화 에러를 최소화 하는 **최고화 모델 $f$**를 찾는 것
  - $f* = arg\,min_{f \in F} R(f)$
    - 실제 위험도를 최소화 하게
- 새로운 데이터의 loss의 평균값이 제일 낮도록

### 경험적 위험도(empirical risk)
- 일반적으로 실제 환경 데이터의 확률 분포 $P(x,y)$를 알지 못함
  - 즉 **실제 위험도**을 알 수 X
- 그렇기 때문에 **경험적 위험도**를 대신 최소화하여 근사
  - $R_{emp}(f) = \frac{1}{n} \sum_{i=1}^{n} L(f(x_i), y_i)$
  - $\hat{f} = arg \, min_{f \in F} R_{emp} (f)$
- 이러한 최소화 하는 과정을 **경험적 위험도 최소화**(ERM; empirical risk minimization) 이라고 함
- 그러나 **경험적 최소화 = 근사**
  - 실제 위험도의 최소화를 의미하지 않음
  - 이는, 모델 검증을 위해 Train외에 **Valid/Test**를 따로 두는 이유

### 모델 학습을 진행하고 목표한대로 나왔는지 확인하는 과정
- training error를 작게
  - **경험적 위험도**를 줄임
- test error와 training error의 차이를 작게
  - 실제 위험도(true risk)와 training error를 작게
- underfit, overfit 발생 여부
  - underfit: training error가 충분히 작지 않을때
  - overfit: training error와 test error의 차이가 클 때
- underfit, overfit 발생시 대응 방법
  - 모델의 수용량(model capacity)를 조절

### 모델 수용량 조절
- 모델을 의미하는 $f \in F$에서 $F$를 조절함
  - 다항의 차수(e.g. 1차, 2차, 3차)를 조절함
- $F$
  - 가설(모델) $f$가 될 수 있는 모든 경우를 나타내는 집합
  - 가설 공간(hypothesis space)
- e.g. 2차원으로 가정하면
  - 모델의 학습 가능하여 최적화 가능한 부분이 $\theta$라고 한다면,
  - $f(\theta)$가 될 수 있는 모든 공간을 **가설 공간**이라고 함
  - $f(\theta) = \hat{y} = b + \theta \, x$
- $F$(가설 공간)을 조절한다
  - 다항식의 차수
    - $f(\theta) = \hat{y} = b + \theta_1x + \theta_2x^2$(다항식의 차수 변경)
  - e.g. ANN(Artificial NN)이라면, layer의 깊이, 한 레이어에서 뉴런의 수 등을 의미
- 간단한 모델(capacity)가 낮을 수록 generalize가 잘 되지만,
  - 보다 나은 성능을 위해 **적합한 복잡성**을 가진 모델을 골라야 함
- 전형적으로 **모델 복잡성**이 커질수록
  - **train error**는 한계까지 계속 내려감
- ![image](https://user-images.githubusercontent.com/10006290/233983192-a49ff695-0cfb-419a-a7e8-162087e6bca0.png)
  - Optimal Capacity를 전후로 `Underfitting zone, Overfitting zone`이 나뉨
- 모델을 쌓으면 쌓을수록 성능은 좋아지나, Ganeralization gap이 커짐
