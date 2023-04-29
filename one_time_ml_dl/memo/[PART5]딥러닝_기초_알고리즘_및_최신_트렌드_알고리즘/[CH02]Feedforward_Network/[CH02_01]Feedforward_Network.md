## CH02_01. Feedbackforward Network

### feed-forward?
- 다층 퍼셉트론(multi-layer perception; MLP)
- 합성곱 신경망(convolutional network; CNN)
- 셀프 어텐션(self-attention)

#### c.f. feed-back
- deconvolutional network

#### c.f. bi-directional
- 중첩 오토인코더(stacked auto-encoders)
- 깊은 볼츠만 머신(deep boltzmann machine)

### 변형 함수(transformation function)의 선택
- 데이터의 표현형(representation) 혹은 feature를 알기 위한 변형 함수(transformation function)의 선택 방법

#### 1. 직접 함수를 디자인(hand-craft)
- 딥러닝 이전에는 일반적

#### 2. 포괄적인 함수를 고름(i.e. kernel function)
- 커널 방법
  - 목표가 이상적인 모델의 확률 밀도 $p(x)$를 구할 때,
  - 일정 단위 안에 **우리가 원하는 데이터가 몇 개 있을지 포함**하는 것
  - $K$가 region안에 들어가는 데이터 수
  - $V$가 region의 크기(부피)
  - $N$이 데이터 수라면, 다음 식과 비례
    - $p(x) \approx \frac{K}{NV}$
  - 이때, $N$은 기본적으로 고정이므로,
    - $K$와 $V$를 조정하여 $p(x)$를 구하는 시도 가능
  - 그 중, $V$를 고정하고 $K$를 찾아냄으로써
    - $p(x)$를 찾는 방식이 커널 방법

#### 3. 딥러닝이 변형 함수 자체를 학습하게 함
- 이 경우, 변형 함수는 **비선형**(non-linear)이어야 함

### 비선형적 변형이 왜 필요할까?
- non-linear transform
- AND, OR 연산에 대해 선형 함수로 구분이 가능하나,
- XOR 연산은 선형 함수로 분류 불가
  - <img width="825" alt="image" src="https://user-images.githubusercontent.com/10006290/235276132-e6968d4f-0711-4974-8b7e-7fde00c3a163.png">

#### VC 차원(Vapnik-Chevonekis Dimension)
- VC-dimension
- $VC(H)$
  - $H$라는 분류기(정확히는 hypothesis set)에 의해
  - 최대로 부술(shatter) 수 있는 point 수
- 선형 분류기의 VC 차원 = **(n+1)차원**
  - 3개 이상 일직선으로 겹치는 점이 3개일때(1차원) -> 1+1 = 2
    - `VC차원 < 점수`, 불가한 경우 발생
  - 3개 이상 일직선으로 겹치지 않는 점이 3개일 때 -> 2+1 = 3
  - 3개 이상 일직선으로 겹치지 않는 점이 4개일 때 -> 2+1 = 3
    - `VC차원 < 점수`, 불가한 경우 발생

### 활성 함수(activation function)
- 하나의 큰 변형함수

### 숨은 유닛(hidden units)
- 앞단의 input unit, 혹은 전단계의 hidden unit으로부터
- 선형으로 변형(affine transform)을 받은 뒤,
- 활성 함수(activation function) 등으로
- **비선형**(non-linear) 변형을 함
  - c.f. 선형 변형: $wx + b$
- Output unit도 hidden unit과 같은 역할 수행 가능
- <img width="501" alt="image" src="https://user-images.githubusercontent.com/10006290/235276839-27129a73-75a4-4870-a78b-3ddebef35f71.png">

### 비선형 활성함수(non linear activation function)

#### tanh
- $z=Wx + b, f(z) = tanh(z)$
- `-1 ~ 1`
- `0`이 중심
  - Bias shift가 없음
- sigmoid처럼 Saturation 문제
  - **gradient vanishing**
    - 중첩하여 사용하게 되면, 1에 가깝게 수렴하게 됨
    - sigmoid도 동일한 문제 존재
    - 중첩할수록 변화가 없어짐

#### ReLU
- Rectified linear unit; 정류 선형 유닛
- $f(z) = max(0,z)$ where $z = Wx + b$
- x가
  - 0보다 크면 선형
  - 0보다 작으면 0

##### 장점
- **쉽계 계산(gradient)이 됨(0 or 1)**
- **Sparsity**: 희박하게(sparse) 활성화 가능
  - 값이 0인 부분이 많으므로, 많은 연산이 줄어짐
- Sigmoid, Tanh 등 함수는 **포화 상태**가 되기 쉬운 반면 **ReLU**는 그러지 않음
  - Sigmoid등은 Layer가 쌓이면, gradient가 중첩
  - 점점 gradient가 0으로 가까워짐
  - 즉, gradient가 사라지는 **gradient vanishing** 문제 발생(추후 자세히 다룸)

##### 단점
- **Unbounded**
  - 무한대(nan) 값이 나올때 본 현상을 막을 수 X
- **0이 중심이 아님**
  - 활용도가 제한될 수 있음
  - weight의 업데이트가 항상 같은 방향으로만 일어남
- **Dying ReLU 문제**
  - Layer가 매우 깊거나, learning rate가 잘못 세팅되면
    - 용량을 차지하거나 항상 죽어있는 문제 발생
    - 이 역히 gradient vanishing
  - Generalize된 ReLU함수를 쓰면 조금 해결
    - 단, 퍼포먼스는 경우에 따라 더 떨어질 수 있음

#### 개선 ReLU: Leaky ReLU
- $z=Wx+b$
  - $f(z) = max(0,z)$, if $z \ge 0$
  - $f(z) = \alpha max(0,z)$, if $z \lt 0$
- 성능상 손해볼 수 있으나,
  - saturation, dying ReLU 문제 완화
- ReLU 대비 데이터가 적을 때 Overfitting 가능성 존재

#### 개선 ReLU: ELU
- exponential Linear Unit
- $z=Wx+b$
  - $f(z) = z$ if $z \ge 0$
  - $f(z) = \alpha(exp(x) - 1)$ if $z \lt 0$
- Leaky 보단 자연스럽게 바꿈
- 일반적으로 가장 효과가 좋음

#### 개선 ReLU: Maxout Units
- $g(z) = max_{z \in K} \, z_i$
- $z$를 다른 $k \in K$값으로 넣고, 각각의 유닛들의 max 값을 취한 형태
- Universal approximation theorem이 볼록 함수(convex)로 점차 근사함을 나타냄
- <img width="579" alt="image" src="https://user-images.githubusercontent.com/10006290/235277705-a429059e-88c4-4537-a7a2-8c32381e3048.png">

### 목적함수: 비용 함수(cost function)와 출력 유닛(output unit)
- ANN을 최적화 하기 위한 목적 함수
  - 즉, cost function은
  - 보통 **가능도함수**를 **최대화**(maximum likelihood) 방법 선택
- $x,y~p_{data}$이고,(x: input, y: output(label))
  - $\theta$가 학습 가능한 파라미터 일때,
  - 모델이 추론하는 **확률 분표**를 $q(y|x;\theta)$라고 한다면,
- 비용함수는 다음과 같이 정의됨
  - $J(\theta) = -E_{x,y~p_{data}}log \, q_{model}(y|x;\theta)$
  - 이는 cross entropy
- cross entropy
  - $H(P,Q) := \sum_i \, p_i log_2 \frac{1}{q_i} = - \sum_i p_i log_2 q_i$
- **MLE**(최대 가능도) 기반의 **비용 함수**를 그대로 사용한다면,
  - $p_{data}$는 데이터의 값으로 바꿀 수 없는 값
  - 우리가 해야하는 것은 $q_{model}(y|x;\theta)$를 구하는 것으로 압축할 수 있음
  - **결과적으로 모델링을 잘 하는 것**

### 출력 유닛(output unit) activation의 종류(필수)

#### 선형(linear)
- 보통 출력 값이 **conditional gaussian distribution**과 같은 확률 분포이거나 **regression**문제 일때 종종 사용됨
- activation function을 사용해 nomalization을 하지 않는 경우

#### 시그모이드(sigmoid)
- $f(x)=sigmoid(x) = \frac{1}{1+e^{-x}}$
- binary classification일 때 많이 사용

#### 소프트맥스(softmax)
- $f(x)=softmax(x_i) = \frac{exp(x_i)}{\sum_{k=1}{K}exp(x_k)}$, for $i=i,...K$
- multi-class classification 일 때 많이 사용
- `0~1`사이로 합이 `1!`
- `K=2`, sigmoid와 동일

### output unit의 activation 종류
- 모델의 목적이 달라지면, output 형식도 다를 수 있음

#### 혼합 밀도(mixture density)
- Gaussian 분포의 혼합을 출력
- <img width="620" alt="image" src="https://user-images.githubusercontent.com/10006290/235327405-ac72937e-9cc9-4ca3-80f8-90f9160eb1a0.png">
- $q_{model}(y|x)=\sum_i^n \, q(c=i|x) N (y; \mu^i(x), \sum^i(x))$
- 일반 아웃풋인 $q(c=i|x)$뿐 아니라,
  - 가우시안 분포를 위한 **평균** 및 **표준편차**도 같이 예측해야 함
- 언제 사용하는가
  - 데이터의 **노이즈성**에 견디기 위한 디자인 중 하나
  - AI모델의 **불확정성 정도**를 처리하기 위해
    - uncertainly level도 같이 출력
    - 설명가능한 AI
  - 컨트롤 가능한 AI
    - exact한 값이 아닌 어느정도 모델을 조절하고 싶을 때

### Feedforward network의 학습

#### 지도 학습적인 접근
- 일반적인 경우, label이 충분할 때
- parameter를 랜덤으로 초기화
- 주어진 label로 loss를 최소화하게 학습
- Stochastic gradient descent와 backpropagation이 쓰임
- 실습 예정

#### 레이블 샘플이, 실제 데이터와 비교했을 때 비율이 작을 때
- 비지도 학습 + 일부분(top)만 지도학습
  - 각각의 layer를 **비지도 학습**으로 학습
  - 그 이후 **지도학습**을 하기 위한
    - **분류기 layer**를 다른 layer를 유지한(fixed)채로 붙임
- 비지도 학습 이후 글로벌하게 지도학습 fine-tune 접근
  - 각각의 layer를 **비지도학습**으로 학습
  - 그 이후 지도학습을 하기 위한 **분류기 layer**를 붙이고 완전히 다시 학습

### Feedforward netowrk의 학습 절차
- <img width="457" alt="image" src="https://user-images.githubusercontent.com/10006290/235327545-d3e64630-b548-46a8-9612-8797469616c9.png">

#### Feed-forward step
- input이 모델로 들어가고, output이 생성
- 생성된 결과를 label과 비교하여 error를 계산
- Train, Test 공통

#### Backpropagation step(역전파)
- Chain rule을 이용하여 gradient들을
  - 학습 가능한 파라미터들에게 업데이트
- 자세한 프로세스는 Theory Session에서 다룸

### Computation Cost, Memory Cost
- 각 cost들은 **Forward step**과 **Backward step**을 따로 고민
  - Forward step -> 학습 뿐만이 아니라, 서비스 퍼포먼스에도 직결
  - Backward step -> Online으로 학습을 돌리는 상황이 아니라면, 학습 속도에만 영향
- 다중 perceptron의 경우 computation cost는 matrix 값을 곱하는 것에서 나옴
- 이 계산과 입력부분의 계산을 제외하고,
  - **Forward step**에서 각 weight matrix를 더하기 위해서는 `O(w)`만큼의 비용이 듦
  - **Backward step**에서도 마찬가지로, 같은 비용인 `O(w)`만큼의 비용이 듦
- 메모리 코스트는 `O(mh)`으로
  - `m`은 `minibatch`의 예제 수
  - `h`는 `hidden units`의 수

### Computational graph(산출 그래프)
- computation을 그래프로 나타냄
- <img width="503" alt="image" src="https://user-images.githubusercontent.com/10006290/235327651-edf71ccb-9fb0-49f3-b87a-c3668248b450.png">
- TensorBoard에서 어느정도 그려줌
