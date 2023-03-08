## CH05_02. (이론강의) Computations of Conv Layers

### Window Extraction

#### Windows(1D)
$$
\vec{x} = \begin{matrix}(x_0 & x_1 & x_2 & x_3 & x_4 & x_5)\end{matrix}
$$
$$
W_0 = X[0:3] = \begin{matrix}(x_0 & x_1 & x_2)\end{matrix}
$$
$$
W_1 = X[1:4] = \begin{matrix}(x_1 & x_2 & x_3)\end{matrix}
$$
$$
W_i = \begin{matrix}(\vec{x}_{i} & \vec{x}_{i+1} & \vec{x}_{i+2})\end{matrix}
$$

- 1씩 이동하면서 형상 비교

#### Windows(2D)
$$
X = \begin{pmatrix}
X[0,0] & X[0,1] & X[0,2] & X[0,3] \\
X[1,0] & X[1,1] & X[1,2] & X[1,3] \\
X[2,0] & X[2,1] & X[2,2] & X[2,3] \\
X[3,0] & X[3,1] & X[3,2] & X[3,3] \\
\end{pmatrix}
$$
$$
W_{0,0} = X[0:3, 0:3] = \begin{pmatrix}
X[0,0] & X[0,1] & X[0,2] \\
X[1,0] & X[1,1] & X[1,2] \\
X[2,0] & X[2,1] & X[2,2] \\
\end{pmatrix}
$$
$$
W_{0,1} = X[0:3, 1:4] = \begin{pmatrix}
X[0,1] & X[0,2] & X[0,3] \\
X[1,1] & X[1,2] & X[1,3] \\
X[2,1] & X[2,2] & X[2,3] \\
\end{pmatrix}
$$
$$
W_{1,0} = X[1:4, 0:3] = \begin{pmatrix}
X[1,0] & X[1,1] & X[1,2] \\
X[2,0] & X[2,1] & X[2,2] \\
X[3,0] & X[3,1] & X[3,2] \\
\end{pmatrix}
$$
- 이미지 사이즈에 따라 관련 내용이 정해짐

$$
W_{i,j} = \begin{pmatrix}
X[i, j] & X[i,j+1] & X[i,j+2] \\
X[i+1,j] & X[i+1,j+1] & X[i+1,j+2] \\
X[i+2,j] & X[i+2,j+1] & X[i+2,j+2] \\
\end{pmatrix}
$$

#### Window Formularization
$$
X \in R^{n_H \times n_W}, W_{i,j} \in R^{f \times f}
$$
$$
X = \begin{pmatrix}
X[0, 0] & X[0,1] & ... & X[0, n_w-f] & ... & X[0, n_W-1] \\
X[1, 0] & X[1,1] & ... & X[1, n_w-f] & ... & X[1, n_W-1] \\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots \\
X[n_H-f, 0] & X[n_H-f,1] & ... & X[n_H-f, n_w-f] & ... & X[n_H-f, n_W-1] \\
X[n_H-1, 0] & X[n_H-1,1] & ... & X[n_H-1, n_w-f] & ... & X[n_H-1, n_W-1] \\
\end{pmatrix}
$$
$$
W_{i,j} = X[i:i+f, j:j+f] = \begin{pmatrix}
X[i, j] & X[i,j+1] & ... & X[i,j+(f-1)] \\
X[i+1, j] & X[i+1,j+1] & ... & X[i+1,j+(f-1)] \\
\vdots & \vdots & \vdots & \vdots \\
X[i + (f-1), j] & X[i + (f-1),j+1] & ... & X[i + (f-1),j+(f-1)] \\
\end{pmatrix}
$$
$$
0 \le i \le n_H-f, 0 \le j \le n_w -f
$$
- $f \times f$의 matrix가 설정됨

### Computations of Conv Layers
$$
W_0 = \begin{matrix}(x_0 & x_1 & x_2)\end{matrix}
$$
$$
K = \begin{matrix}(k_0 & k_1 & k_2)\end{matrix}
$$
- $W_0$를 $K$에 correlation(filtering) 수행

$$
z_0 = W_0 \bigotimes K + b
$$

$$
W_1 = \begin{matrix}(x_1 & x_2 & x_3)\end{matrix}
$$
$$
K = \begin{matrix}(k_0 & k_1 & k_2)\end{matrix}
$$
$$
z_1 = W_1 \bigotimes K + b
$$
- 위 값을 4개로 만들어 보면,

$$
(\vec{z})^T = \begin{matrix}
  (z_0 & z_1 & z_2 & z_3)
\end{matrix}
$$

- 2차원에서도 동일한 연산 수행

#### 일반화
$$
X \in R^{n_H \times n_W}, W_{i,j} \in R^{f \times f}, K \in R^{f \times f}, b \in R
$$
$$
Z[i,j] = W_{i,j} \bigotimes K + b
$$
$$
Z = Conv2D(X; K,b) = \begin{pmatrix}
W_{0,0} \bigotimes K + b & W_{0,1} \bigotimes K + b & ... & W_{0,n_W-f} \bigotimes K + b \\
W_{1,0} \bigotimes K + b & W_{1,1} \bigotimes K + b & ... & W_{1,n_W-f} \bigotimes K + b \\
\vdots & \vdots & \vdots & \vdots \\
W_{n_H-f,0} \bigotimes K + b & W_{n_H-f,1} \bigotimes K + b & ... & W_{n_H-f,n_W-f} \bigotimes K + b \\
\end{pmatrix}
$$

#### Convolution layer를 통과했을때 size
$$
n`H = n`_H -f +1
$$
$$
n`W = n`_W -f +1
$$

#### Activation Layer 통과
$$
Z[i,j] = W_{i,j} \bigotimes K + b
$$
$$
A[i,j] = \sigma{(Z[i,j])}
$$
$$
A = Conv2D(X; K,b; \sigma) = \begin{pmatrix}
\sigma{(W_{0,0} \bigotimes K + b)} & \sigma{(W_{0,1} \bigotimes K + b)} & ... & \sigma{(W_{0,n_W-f} \bigotimes K + b)} \\
\sigma{(W_{1,0} \bigotimes K + b)} & \sigma{(W_{1,1} \bigotimes K + b)} & ... & \sigma{(W_{1,n_W-f} \bigotimes K + b)} \\
\vdots & \vdots & \vdots & \vdots \\
\sigma{(W_{n_H-f,0} \bigotimes K + b)} & \sigma{(W_{n_H-f,1} \bigotimes K + b)} & ... & \sigma{(W_{n_H-f,n_W-f} \bigotimes K + b)} \\
\end{pmatrix}
$$
- 하나씩 윈도우를 가지고 함수를 통과시킨 형태
