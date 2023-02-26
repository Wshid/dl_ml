## CH04_01. (이론강의) Mean Squared Error
- Loss 3가지중 하나

### Loss가 왜 필요한가?
- Loss가 왜 필요한가?
$$
\vec{x}^T -> Model -> \hat{y}
$$
- 이때 $\hat{y}$를 Regression이라고 함
  - Regression은 보통 실수 값
- Regression을 특정 숫자 값으로 descrete하게 추상화하여 클래스를 구분하면, 이는 **classtification**
  - e.g. 0 -> 강아지, 1 -> 고양이, 2 -> ...
- classification의 경우 **대소관계는 존재하지 x**
- 이 모델학습 과정에서, 실제 $y$값과의 차이 -> Loss
  - 모델의 학습 인자로 활용
- Regression, Classification
  - **Regression**: $\hat{y} \in R$
    - Loss: `MSE`
  - **Classification**: $\hat{y} \in C$, {0, 1, 2, ... k}
    - Loss(Binary.): `Bino`
    - Loss(Multi.): `Catergorical`

### Cartesian Product for Predictions/Labels
- 집합의 종류
  - $R$
  - $B = \{0, 1\}$
  - $C = \{c_1, c_2, ... c_k\}$
  - $P = \{x|0 <= x <= 1 \}$
  - $B^n_1 = \{(b_1, b_2, ... b_n)^T | \forall b_i \in B, \sum_{i=1}^{n} b_i = 1\}$
    - One-hot vector

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
- 위 내용들을 정리하면,
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
y^(N) \end{pmatrix} \space \in R^{N \times 1}
$$

#### 구하는 공식
- **Squared Error**
  - 실수 사이에서 활용하는 공식
  - $J = (y -\hat{y})^2$
  - $n^{[0]}$에서 Activation을 하지 않은 $\hat{y}$를 바로 사용
- **Mean Squared Error**
  - $J = \frac{1}{N} \sum_{i=1}^{N} (y^{(i)} - \hat{y}^{(i)})^2$
  - Squared Error의 평균
- Loss의 특징
  - 서로 비슷하면 비슷할수록 0에 가까우며
  - 차이가 발생할수록 $\infty$에 가까움
