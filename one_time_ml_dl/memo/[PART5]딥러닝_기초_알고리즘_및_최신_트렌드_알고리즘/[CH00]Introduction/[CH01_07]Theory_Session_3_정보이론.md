## CH01_07. [Theory Session 3] 정보이론

### 정보(information)
- 특정한 관찰에 의해 얼마만큼의 정보를 획득했는지 수치를 정량화한 값
- 사건 A가 발생할 확률을 $P(X)$라 할때, 정보량은 다음과 같음
  - $h(X) := -logP(X)$
  - 정보가 자주 일어나면, 작아짐

#### 엔트로피(Entropy)
- 이산 확률 변소의 **평균 정보량**을 의미
- 클수록 정보량이 많음
- $H[X] := \sum_i^N p_i log_2 \frac{1}{p_i} = -\sum_i^N p_i log_2 p_i$
  - $p_i := P(x=x_i)$
    - prob. information gain

### 쿨백-라이블러 발산(KL-Divergence; KLD)
- **두 확률 분포**의 다른 정도를 나타내는 척도
- **Relative Entropy**라고도 함
  - $D_{KL}(P||Q) := - \sum_i^N p_i log_2 q_i -(-\sum_i^N p_i log_2 p_i) = -\sum_i^N p_i log_2 \frac{q_i}{p_i} = H(P,Q) - H(P)$

#### KL-Divergence의 성질
- $D_{KL}(P||Q) \neq D_{KL}(Q||P)$ (cf. Jensen-Shannon Divergence)
  - 교환법칙이 성립하지 X
- $D_{KL}(P||Q) = 0$, if and only if $p=q$
- $D_{KL}(P||Q) \ge 0$
- Jenson Inequality
  - Convex 한 함수에서 활용 가능

### cross-entropy
- $H(P,Q) := \sum_i p_i log_2 \frac{1}{q_i} = - \sum_i p_i log_2 q_i $
- 만약, 최적이 아닌 다른 확률 분포로 ig(information gain)을 얻었다면,
  - 실제 머신러닝 학습 상황 등
  - $D_{KL}(p_{data} || q_{model}) = E_{x~p_{data}}[log_2 p_{data}(x) - log_2 q_{model}(x)]$
- 왼쪽, data 관련 텀은 모델과 관련이 없는 **데이터 생성 부분**이기 때문에 **단순 분류 문제에서는 생략 가능**
- 즉,
  - $-E_{x~p_{data}}[log_2 q_{model}(x)] = - \sum_i p_{data} log_2 q_{model} = H(P_{data}, Q_{model})$
  - Classification 문제에서는 **cross entropy loss**를 많이 사용