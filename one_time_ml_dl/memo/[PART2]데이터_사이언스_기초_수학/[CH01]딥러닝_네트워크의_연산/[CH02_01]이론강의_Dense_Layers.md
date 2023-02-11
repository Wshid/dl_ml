## CH02_01. (이론강의) Dense Layers

### Neuron Vectors and Layers
- X -> Layer1 -> Layer -> ... -> Prediction
- Layer
  - Neurons가 여러개 나열된 형태
- 기호 표현
  ```bash
  ->v = v1 v2 v3 ... vn # 하나의 Layer, Neuron의 묶음

  # v1, v2 각각 다른 parametric function을 생성함
  # v1, v2 각각 ->w, b 다른 값을 가지고 있음
  # `(->x)^T * ->w + b`는 filtering
  ```
- filter bank
  - filter의 집합
  - x 입력에 따라 v1, v2별로 결과가 달라짐
- cascade 구조
  - 여러 layer로 이루어진 구조

### Dense Layers
```bash
(->x)^T = x1 x2 x3 ... xli
# 위 값이 v1 v2 v3 ... vn과 모두 연결된 것(mesh 형태)
# 하나의 v1이 모든 x1 ... xli
# 하나의 v2이 모든 x1 ... xli
```
- edge, node
  - node: x, v
- vn은 ->w, b 라는 파라미터를 가지고 있음
  - activation func는 파라미터를 가지고 있지 않음(단순 함수)(e.g. sigmoid)
  - 이번 강의에서는 activate func(파라미터를 받지 않아도) layer로 구분

### Notation
- Layer: `L^[i]`
- Neuron Vector: `->v^[i]`
- of Neurons: `li`(l for length)
