## CH02_02. (이론강의) The First Dense Layer

### Params of Dense Layer
```bash
# 뉴런이 li개 있다면, weight도 li개 존재
L^[1] = v1^[1] v2^[1] v3^[1] ... vli^[1]

w_1,1^[1] # column, row
w_2,1^[1]
...
w_li,1^[1]

->x^T => ->w = (w1 w2 ... wli)
```

### Weight Matrix and Bias Vector
- 각개의 weight vector를 하나의 weight maxrix로
- 각개의 bias를 bias vector로 모아 관리
```bash
->w_1^[1] = w_1,1^[1] w_2,1^[1] ... w_li,1^[1]
->w_2^[1] = w_1,2^[1] w_2,2^[1] ... w_li,2^[1]
->w_li^[1] = w_1,li^[1] w_2,2^[1] ... w_li,l1^[1]

# 위 weights들을 matrix로 표현
W^[1] = ->w_1^[1] ->w_2^[1] ... ->w_li^[1] ∈ R^li X l1 # li x l1에 유의 
# li는 input(x)의 벡터에 따라 결정되며
# l1는 뉴런의 갯수(column)에 따라 결정
# bias는 l1개가 생성

# broadcasting을 더 쉽게 하기 위해, 아래와 같이 표현
(->b[1])^T = (b1^[1] b2^[1] ... bli[1]) ∈ R^1 x li
```
- l1의 뉴런들이 존재한다면, l1들의 weight vector가 존재
- bias는 l1만큼 존재

### FP(Forward Propagation) of Dense Layer
- 중요!
```bash
# g는 sigmoid와 같은 activation func
ai^[1] = g((->x^T)->wi[1] + bi^[1]), 1<=i <= li
```
- weight matrix와 bias vector를 통해 FP를 빠르게 할 수 있음
- `x*w + b` 형태를 가짐
- 최종적으로 row vector(`x1 x2 ... xlI`)를 Input으로 가지게 되면
  - (`a1^[1] a2^[1] ... alI^[1]`) 형태의 row vector를 Output으로 가짐

### Dimensions of Dense Layer
```bash
x1 x2 ... xlI ∈ R^1 x lI
W^[1] ∈ R^lI x l1
(->b^[1])^T ∈ R^1 x l1
```
