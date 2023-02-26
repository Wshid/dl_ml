## CH04_02. (이론강의) Binary Cross Entropy

### Dataset for Binary Classification
### Mean Squared Error
- Dataset for Regression
$$
(\vec{x}^{(1)}) = ( x_1^{(1)} x_2^{(1)} \space ... \space x_{l_I}^{(1)} ) \space \space y^{(1)} \in R
$$
$$
(\vec{x}^{(2)}) = ( x_1^{(2)} x_2^{(2)} \space ... \space x_{l_I}^{(2)} ) \space \space y^{(2)} \in R
$$
$$
(\vec{x}^{(N)}) = ( x_1^{(N)} x_2^{(N)} \space ... \space x_{l_I}^{(N)} ) \space \space y^{(N)} \in R
$$
$$
X^T = \begin{pmatrix} 
\leftarrow \space \space \vec{x}^{(1)} \space \space \rightarrow \\
\leftarrow \space \space \vec{x}^{(2)} \space \space \rightarrow \\
\vdots \\
\leftarrow \space \space \vec{x}^{(N)} \space \space \rightarrow \\
\end{pmatrix} \in R^{N \times l_I}
$$
$$
Y = \begin{pmatrix}
y^(1) \\
y^(2) \\
\vdots \\
y^(N) \end{pmatrix} \space \in B^{N \times 1}
$$
- **$Y$가 Binary 집합 하위**

### Binary Cross Entropy
- $H_b$는 바이너리를 의미
$$
H_b(y, \hat(y)) = - [y log(\hat{y}) + (1-y)log(1-\hat{y})]
$$
- $y=0$일 때,
  - $\hat{y} \fallingdotseq 0, L -> 0$
  - $\hat{y} \fallingdotseq 1, L -> \infty$
- 공식 유도
  - $y=1 => L = -log(\hat{y})$
  - $y=0 => L = -log(1-\hat{y})$
- $\hat{y}$자체가 $0, 1$사이인 확률값이어야 함
  - 즉, activation func(sigmoid) 통과가 필요
$$
v^{[0]}, g(z) = \sigma(z), \hat{y} \in P
$$
$$
J = H_b(y, \hat{y})
$$

#### 요약
- Binary Classifier의 Loss계산시
  - 마지막 output layer에 sigmoid를 통과시킴

#### Minibatch
- 각 $L$(Loss)의 평균을 계산
$$
J = H_b(Y, \hat{Y})
$$
$$
\frac{1}{N} \sum_{i=1}^{N} [y^{(i)}log(\hat{y}^{(i)}) + (1 - y^{(i)})log(1-\hat{y}^{(i)})]
$$