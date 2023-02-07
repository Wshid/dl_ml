## CH01_01. (이론강의) Parametric Functions and Datasets

### Parametric Functions
- `f(x)`: 일반적인 함수
  - 입력을 받아 연산을 처리하여 반환
- `f(x; θ)`: Parametric Functions
  ```bash
  # θ는 output을 만들어내는데 필요한 변수
  z = x + θ 
  z = θx
  ```
  - θ가 달라짐에 따라 다른 함수가 만들어짐
  - 같은 모양을 띄고 있으나, 파라미터 값에 따라 역할이 달라짐
  - 함수의 작동 자체가 달라짐
  - **파라미터가 내재된 함수** => 딥러닝의 핵심 개념
  - `θ`는 엄청 많음
- x는 object(vector)자체가 들어오는 값
  - e.g. 2차원 벡터, tensor, ...

### Hierarchy of Tensor Computations
- Tensor
  - vector, scala, metrics를 일반화 하여 표현한 것 

#### Zeroth-order Tensor Operations
- scala
- 실수 하나를 가진 것(R)
- `X`는 Cartesian product를 의미
  - 단순 곱이 아님

#### First-order Tensor Operations
- vector
- 하나의 1차원 형태의 리스트
- first order = tensor = vector
- inner product도 가능

#### Second-order Tensor Operations
- matrixs
- 행렬 곱 가능

#### Third-order Tensor Operations
- `R^2*3*3`

#### Dataset(X Data)
- x 벡터(row vector)
- 각각의 입력은 다음과 같이 표현
  ```bash
  ->x(1) : 첫번째 데이터 벡터
  (->x(1))^T = ( (x1(1))^T (x2(1))^T ... (xn(1))^T ) # length of input, li
  ```
- second order tensor
