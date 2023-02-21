## CH03_02. (이론강의) Softmax Layer
- 마지막 Layer의 Neuron의 수는
  - 구분 하고 싶은 클래스의 수(K)와 일치해야 함
- e.g. 특정 이미지를 주고, 어느 동물인지 구분
  - 호랑이, 강아지, 토끼, 고양이가 있다면
  - 마지막 Layer의 Neuron수는 4여야 함
  - 또한 리턴값은 $P$값이어야 함

### Softmax Layer
$$
l_1 \space l_2 \space \dots \space l_K \\
\text 각각은 z값을 가짐
$$
- 위와 같은 상황에서, `activation function = linear`라면,
  - $f(x)=x$
- 각각의 $l$값은 **각 클래스별** $Logit$값이 됨
- 로직 벡터$(\vec{l})^T$를 대입하면, 다음과 같은 식이 완성됨
  $$
  p_i = P(C_i), 1<= i<= K, \space \space \sum_{i=1}{k} p_i = 1 \\
  \space \\
  p_1 \space p_2 \space \dots \space p_K = (\vec{p})^T \\
  \uparrow \\
  S_j((\vec{l})^T) = p_j = \frac{e^{l_j}}{\sum_{k=1}^{K} [e^{l_k}]} \\ 
  \uparrow \\
  l_1 \space l_2 \space \dots \space l_K = (\vec{l})^T
  $$
- Softmax vector의 특징
  - input은 Logit, K개의 Logit vector를 넣어주게 되면,
  - K개의 Probabilty vector로 변환
- Softmax에 한해서만,
  - $l$은 length가 아닌 `logit`을 의미

#### 핵심
- softmax는
  - **n개의 클래스를 구분**하기 위해서 쓰이며,
  - 이때 마지막 Layer의 neuron 수와 클래스 수는 같고
  - 각각의 값은 확률을 나타냄
  - logit vector -> probability vector
- sigmoid
  - logit 1개 -> 1개의 probability

#### Binary Classification
- 마지막 Layer에 1개의 neuron을 두고 sigmoid를 적용해도 되고,
- 마지막 Layer에 2개의 neuron을 두고 softmax를 적용해도 됨

### from Feature to Prediction
$$
\^{Y^{T}} \\
\uparrow \\
Softmax \\
\space \\
L^{[O]} \\ 
\uparrow \\
\vdots \\
L^{[2]} \\ 
\uparrow \\
L^{[1]} \\ 
\uparrow \\
X^T
$$
- activation function을 통과하지 않고, 바로 $z$값을 Softmax에 투과
- 최종 값은 prediction vector(probability vector)로 변환됨
