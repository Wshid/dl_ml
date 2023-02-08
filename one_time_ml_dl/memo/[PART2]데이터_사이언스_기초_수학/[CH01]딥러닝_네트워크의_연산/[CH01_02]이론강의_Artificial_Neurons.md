## CH01_02. (이론강의) Artificial Neurons
- Affine + Activation

### Affine Functions with One Feature
```bash
# weighted sum
z = xw

# Affine Transformation
z = xw + b(bias) # f(x; w,b)

# Weighted Sum
# Weight에 따라 중요도가 달라짐
z = w1x1 + w2x2 + ... + wnxn # (x)^T * w

# Affine Transformation
z = w1x1 + w2x2 + ... + wnxn + b # (x)^T * w + b
# x와 w의 원소수는 같음
```

### Activation Functions
- Sigmoid
- Tanh
- **ReLU**
  - 가장 많이 사용

### Artificial Neurons
- Affine Function을 거친 이후 Activation을 적용하는 형태
- 최종적으로 Activation Value가 리턴됨

### Minibatch in Artificial Neurons
- 묶음 단위,
  - n개의 입력으로 n개의 z 반환
  ```bash
  # ->W와 b는 동일함
  (->X(1))^T -> a(1) = g((->x^(1))^T * ->W + b)
  (->X(2))^T -> a(2) = g((->x^(2))^T * ->W + b)

  # 위 구조는 아래 형식과 동일
  f(x; θ) = x + θ

  # 여러 x1 ... xn의 값을
  # X로 표현
  X^T -> f(X^T; ->w, b), Affine -> g(z), Activation -> A(Activation Value)
  ```
