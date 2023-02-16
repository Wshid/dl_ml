## CH02_04. (이론강의) Minibatches in Dense Layers

### Minibatch in Dense Layers
- 데이터 샘플이 n개가 들어오는것은, weight, bias에 영향을 미치지 않음
  ```bash
  (->x^(1))^T
  (->x^(2))^T
  ```
- minibatch
  - input이 여러개가 된다는 의미
  - 뉴런들과 연관 x
- Input
  ```bash
  X^T = (x1^(1) x2^(1) ... xlI^(1))
        (x1^(2) x2^(2) ... xlI^(2))
        (...               xlI^(N))

  (Z^[1])^T = ((->x^(1))^T (->x^(2))^T ... (->x^(N))^T) * ->w1^[1] + b1^[1]
  ```
- **Input이 N x ?였다면, Output도 N x ? 형태**
- 일반화
  ```bash
  zi,j^[1] = (->x^(i))^T * ->wj^[1] + bj^[1]
  ```
- 형태의 변화
  ```bash
  X^T ∈ R^N*lI
  W^[1] ∈ R^lI*li
  (b^[1])^T ∈ R^1*li

  # affine, activation을 지난 이후
  ai,j^[1] = g(zi,j^[1])
  ```

### Batch-wise, Neuron-wise
```bash
# 가로는 batch-wise, 동일한 데이터 샘플을 통과한 값
# 세로는 Neuron-wise
(A^[i])^T = (a1,1^[i] a1,2^[i] a1,3^[i] ... a1,li^[i])
            (a2,1^[i] a2,2^[i] a2,3^[i] ... a2,li^[i])
            ...
            (aN,1^[i] aN,2^[i] aN,3^[i] ... aN,li^[i])
```

### Casecaded Dense Layer
```bash
(A^[O])^T) = (A^[O-1])^T) * W^[O] + (->b^[O])^T
...
(A^[2])^T) = (A^[1])^T) * W^[2] + (->b^[2])^T
(A^[1])^T) = X^T * W^[1] + (->b^[1])^T
# R^N*l1 = R^N*lI R^lI*l1 R^1*l1
```
