## CH05_01. (이론강의) Image Tensors and Classical Correlation

### Image Tensors
- 세로를 H(height), 가로를 W(width)로 표현하며
  - `H x W`순으로 지칭
- 이미지는 다음과 같이 표현

$$
X \in R^{n_H \times n_W}
$$

$$
X = \begin{pmatrix}
X[0,0] & X[0,1] & ...  & X[0, n_w -1] \\
X[1,0] &  X[1,1] & ... &  X[1, n_w -1] \\
\vdots &  \vdots &  \vdots  & \vdots  \\ 
X[n_H-1,0] & X[0,1] & ...&  X[n_H -1, n_w -1] \\
\end{pmatrix}
$$
- RGB 채널을 가진다면, 그에 맞는 $n_C$ 채널이 추가됨

$$
X \in R^{n_H \times n_W \times n_C}
$$
- 4차원으로 확장(이미지가 여러개일 경우)

$$
X \in R^{N \times n_H \times n_W \times n_C}
$$

### Correlation
- Conv와 혼용해서 사용함

#### Classical Correlation
- Filter가 추가됨

$$
X \in R^{n_H \times n_W}, F \in R^{n_H \times n_W}, z \in R
$$
- correlation의 표현은 다음과 같음
  - 같은 위치의 elements를 곱해서 더하는 형태

$$
z = X \bigotimes F = \sum_{i=0}^{n_H-1} \sum_{i=0}^{n_W-1} X[i,j] F[i,j]
$$
$$
X \bigotimes F : R^{n_H \times n_W} \times R^{n_H \times n_W} \rightarrow R
$$
- 예시, 만약 $n_H=3, n_W=3$ 일때,

$$
X = \begin{pmatrix}
X[0,0] & X[0,1] & X[0,2] \\
X[1,0] & X[1,1] & X[1,2] \\
X[2,0] & X[2,1] & X[2,2] \\
\end{pmatrix}
$$

$$
F = \begin{pmatrix}
F[0,0] & F[0,1] & F[0,2] \\
F[1,0] & F[1,1] & F[1,2] \\
F[2,0] & F[2,1] & F[2,2] \\
\end{pmatrix}
$$
$$
z = X \bigotimes F = \sum_{i=0}^{2} \sum_{i=0}^{2} X[i,j] F[i,j]
$$
$$
X[0,0]F[0,0] + X[0,1]F[0,1] + X[0,2]F[0,2] + ... + X[2,2]F[2,2]
$$

#### Correlation with Bias
- 마지막 bias만 더해주면 됨

$$
z = X \bigotimes F+ b = \sum_{i=0}^{n_H-1} \sum_{i=0}^{n_W-1} X[i,j] F[i,j] + b
$$
$$
X \bigotimes F + b : R^{n_H \times n_W} \times R^{n_H \times n_W}  + R \rightarrow R
$$

#### Convolution
- Correlation을 한번 회전하여 filtering을 거는 형태
  - Correlation: 두 신호의 유사성을 측정해주는 도구

$$
X = \begin{pmatrix}
X[0,0] & X[0,1] & X[0,2] \\
X[1,0] & X[1,1] & X[1,2] \\
X[2,0] & X[2,1] & X[2,2] \\
\end{pmatrix}
$$
$$
F = \begin{pmatrix}
F[2,2] & F[2,1] & F[2,0] \\
F[1,2] & F[1,1] & F[1,0] \\
F[0,2] & F[0,1] & F[0,0] \\
\end{pmatrix}
$$

#### Correlation with Activation
- activation은 보통 Relu 사용

$$
a \\
\uparrow \\
a = g(z) \\
\uparrow \\
z = X \bigotimes F + b \\
\uparrow \\
X
$$

#### Correlation and Dot Product
$$
X = \begin{pmatrix}
A[0,0] & A[0,1] & A[0,2] \\
A[1,0] & A[1,1] & A[1,2] \\
A[2,0] & A[2,1] & A[2,2] \\
\end{pmatrix}
$$
- 위 matrix를 flatten하게 펼치면, 1차원 리스트가 됨
>  $flatten(X) \in R^9$ 
- 해당 리스트로 생각했을 때 계산식은 아래와 같음

$$
\sum_{i=0}^{n_H-1} \sum_{i=0}^{n_W-1} X[i,j] F[i,j] + b = (flatten(x))^T flatten(F) + b
$$
