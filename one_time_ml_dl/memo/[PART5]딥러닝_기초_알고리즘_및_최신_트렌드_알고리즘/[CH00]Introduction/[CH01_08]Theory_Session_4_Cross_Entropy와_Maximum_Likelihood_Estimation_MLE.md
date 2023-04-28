## CH01_08. [Theory Session 4] Cross Entropy와 Maximum Likelihood Estimation(MLE)

### 로지스틱 회귀로 이항 분류(classification)
- sigmoid와 같은 activation function을 통해 0~1로 값 정의
  - 이후 중간값인 0.5를 기준으로 0,1로 값 정의
- Log Likelihood(로그 우도법)

### 일반화
- n개의 샘플을 가진 데이터 $X ~ {x_1, ... x_n}$이 있을때,
  - 이를 독립적으로 생성하는 **데이터 생성 확률 분포를** $p_{data}$
  - 매개 변수 $\theta$(튜닝가능한)을 가지는 **모델의 예측 분포**를 $q_{model}$이라면
  - $\theta$의 **최대 가능도 추정**(maximum likelihood estimator)는 아래를 만족함

$$
\theta_{MLE} =  arg \, max_{theta} \, q_{model}(X;\theta) = \prod_i^n q_{model} (x_i; \theta)
$$

- 최적화를 좀 더 편하기 위해 log를 씌우면

$$
arg \, max_{\theta} \sum_i^m log \, q_{model} (x_i;\theta)
$$

- 위 값을 최적화 하는 문제로 변경 됨
- 여기에 데이터를 놓고, 결과적으로 평균을 내는 작업을 하게 되면 아래를 만족함

$$
arg \, max_{\theta} \, E_{x~p_{data}} \, log \, q_{model} (x;\theta) = arg \, min_{\theta} \, H[p_{data}(x), q_{model}(x;\theta)]
$$

- 결국, **KL-divergence**를 생각하면, $p_{data}$와 모델$q_{model}$ 사이의 **비유사성**(dissimilarity)를 줄이게 됨
