## CH02_03. (이론강의) Generalized Dense Layers

### Dimensions of Dense Layers
```bash
(->x)^T ∈ R^1*li
```

### The Second Dense Layer
- mxnet
  - gpu를 여러개 돌릴때 최적화된 라이브러리
  - parameter: include_top과 연관
    - 밑에서 위로 전파되는것을 의미
```bash
# 아래 레이어의 결과는 a1^[2] a2^[2] ... al2^[2]
v1^[2] v2^[2] v3^[2] ... v1^[2] # L^[2]
v1^[1] v2^[1] v3^[1] ... v1^[1] # L^[1]
```

### The Params of The Second Dense Layer
```bash
R^1*li
->wi^[2] = (wl,i^[2] w2,i^[2] w3,i^[2] ... wl1,i^[2])
```
- 파라미터의 수
  - L1: `l1(li + 1)`
  - L2: `l2(l1 + 1)`
- 뉴런 하나만 증가하더라도, 파라미터가 기하급수적으로 증가

### FP of The Second Dense Layer
```bash
ai^[2] = g((->a[1])^T * ->wi^[2] + bi^[2]) # 1<=<=l2
vi^[2]((->a^[1])^T; ->wi^[2], bi^[2])
```
- 첫번째 layer의 output은 두번째 레이어의 input

### Generalized Dense Layer
```bash
(->a^[i-1])^T ∈ R^1*li-1 # input
->v^[i]((->a^[i-1])^T) # layer
(->a^[i])^T ∈ R^1*li # output

# i번째 layer의 v1 weight
->w1^[i] = (w1,1^[i] w2,1^[i] w3,1^[i] ... wi-1,1^[i]) ∈ R^li-1*1 

# i번째 layer의 v2 weight
->w1^[i] = (w1,2^[i] w2,2^[i] w3,2^[i] ... wi-1,2^[i]) ∈ R^li-1*1 

# i번째 인덱스, 뉴런이 li개 있기 때문
->wli^[i] = (w1,li^[i] w2,li^[i] w3,li^[i] ... wi-1,li^[i]) ∈ R^li-1*1 

# 최종적으로.. li개의 뉴런이 있다면
R^li-1*li 
```