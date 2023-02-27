## CH04_03. (이론강의) Categorical Cross Entropy

### Dataset for Multi-class Classification
$$
C = \{ c_1, c_2, ... , c_K\}
$$

#### Dataset for Multi-class Classification + One-hot Encoding
- one-hot vector
  $$
  (\vec{y}^{(i)})^T \in B_1^{1 \times K}
  $$
  - 예시
    - `1 0 0 0 0 ...`: 강아지
    - `0 1 0 0 0 ...`: 토끼

### Categorical Cross Entropy
$$
(\vec{y})^T = (y_1 y_2 ... y_K)
$$
$$
(\vec{\hat{y}})^T = (y_1 y_2 ... y_K)
$$
$$
J = H(\vec{y}, \vec{\hat{y}}) = - \sum_{i=1}^{K} y_i log(\hat{y}_i)
$$
- One-hot vector에서는 하나만 1값을 가짐
  - 그에따라, $P(C_k)$값이 높아야 score가 높음
- Loss 계산
  - Softmax를 통과한 값: $(\vec{\hat{y}})$
  - One Hot Vector: $(\vec{y})$
  - 이 둘에 `J` 공식을 사용
- Minibatch의 경우에도 동일함

### from Feature to Loss
$$
X^T -> L^{[1]} -> L^{[2]} -> ... -> L^{[O]} -> Softmax -> Cross Entropy -> J
$$
- 반대방향은 미분값 활용
