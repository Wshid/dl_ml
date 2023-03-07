## CH03_01. (이론강의) Logit and Sigmoid
- Loss
  - model의 예측, 실제 값의 차이
  - 이 차이를 줄여나가게 학습
- Sigmoid, Softmax
  - Image Classification에서 많이 쓰임
- CV, NLP: 딥러닝이 많이 사용되는 분야
  - CV(Computer Vision)은 IC와 연관
  - NLP는 RNN 중심

### Odds
- 두가지 경우가 있었을 때 확률을 표현하는 방법
  - $o=\frac{p}{1-p}$
  - e.g. 뒷면 나올 확률 대비, 앞면이 나올 확률
- 확률이 0.5일 경우, 값이 1

### Logit
- Odds에 $Log$를 씌운 값
  - $l = log(\frac{p}{1-p})$
- 확률이 0.5일 경우 값이 0이 됨
- 위/아래로 대충되는 그래프
- 값의 범위는 $-\infty < logit < \infty$를 가짐

### Logit and Sigmoid
- $l$은 $logit$을 의미
$$l = log(\frac{p}{1-p})$$
$$e^l = \frac{p}{1-p} $$(양변에 log를 없애기 위해 Exponential 추가) 
$$\frac{1}{e^l} = \frac{1-p}{p}=\frac{1}{p}-1$$
$$\frac{1}{e^l}+1=\frac{1}{p}$$
$$\frac{1+e^l}{e^l}=\frac{1}{p}$$
$$p=\frac{e^l}{1+e^l}$$
$$p=\frac{1}{1+e^-l}$$
$$p=\sigma{(l)}=\frac{1}{1+e^-l}$$
- sigmoid와 같은 형상
- 확률을 입력 받아, logit으로 변환 -> logit 함수
- logit을 받아 확률로 변환 -> logit의 역함수, sigmoid
- $0 < sigmoid < 1$
- $-\infty < (\vec{x})^T \cdot > \vec{w}+b = z < \infty$
  - $z$값을 logit으로 다룰 예정(Alfine func.)
  - logit을 통과하게 되면 확률 $p$로 변환 가능
- 결국 확률을 내보내는(예측률) 방법으로 활용 가능
- sigmoid는 확률로 계산하기 위한 도구

### from Logit to Probability
$$(\vec{x})^T$$
$$z=(\vec{x})^T \cdot \vec{w} + b $$ 
$$-\infty < z < \infty$$
$$ p = \frac{1}{1+e^-z}$$
$$0 <= p <= 1$$
- logistic regression에서 자세히 다루게 될 내용

#### X 확장
$$
X^T = \begin{pmatrix} \longleftarrow (\vec{x}^(1))^T \longrightarrow \\ \longleftarrow(\vec{x}^(2))^T \longrightarrow\\ ... \\ \longleftarrow(\vec{x}^(N))^T \longrightarrow\end{pmatrix}
$$
$$
\vec{z}^{[1]} = X^T \vec{w}^{[1]} + b^{[1]} \\
\vec{p} = \frac{1}{1 + e^-\vec{z}^{[1]}}
$$
- 각 값이 포함되는 범위 
$$
b^{[1]} \in R \\
\vec{w}^{[1]} \in R^{l_I} \\
\vec{z}^{[1]} \in R^{[N \times 1]} \\
\vec{p} \in R^{[N \times 1]}
$$
