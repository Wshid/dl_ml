## CH05_03. (이론강의) Conv Layers for Multichannel Input

### n-Channel Input
$$
X \in R^{n_H \times n_W \times n_C}
$$
- RGB의 input을 포함한 이미지는, 3차원의 tensor를 가짐

$$
X[:,:,0]
$$
$$
X[:,:,1]
$$
$$
X[:,:,2]
$$

#### Windows
$$
f = 3, n_C = 3, W_{i,j} \in R^{3 \times 3 \times 3}
$$

- Red, Green, Blue에 해당하는 Layer

$$
W_{i,j} = X[i:i+f,j:j+f,0] =\begin{pmatrix}
X[i, j,0] & X[i,j+1,0] & X[i,j+2,0] \\
X[i+1,j,0] & X[i+1,j+1,0] & X[i+1,j+2,0] \\
X[i+2,j,0] & X[i+2,j+1,0] & X[i+2,j+2,0] \\
\end{pmatrix}
$$

$$
W_{i,j} = X[i:i+f,j:j+f,1] =\begin{pmatrix}
X[i, j,1] & X[i,j+1,1] & X[i,j+2,1] \\
X[i+1,j,1] & X[i+1,j+1,1] & X[i+1,j+2,1] \\
X[i+2,j,1] & X[i+2,j+1,1] & X[i+2,j+2,1] \\
\end{pmatrix}
$$

$$
W_{i,j} = X[i:i+f,j:j+f,0] =\begin{pmatrix}
X[i, j,2] & X[i,j+1,2] & X[i,j+2,2] \\
X[i+1,j,2] & X[i+1,j+1,2] & X[i+1,j+2,2] \\
X[i+2,j,2] & X[i+2,j+1,2] & X[i+2,j+2,2] \\
\end{pmatrix}
$$

- Kernel의 경우에는 다음과 같이 존재(Red)

$$
K[:,:,0] = \begin{pmatrix}
K[0,0,0] & X[0,1,0] & X[0,2,0] \\
K[1,0,0] & X[1,1,0] & X[1,2,0] \\
K[2,0,0] & X[2,1,0] & X[2,2,0] \\
\end{pmatrix}
$$

### Conv Layers
- `3`으로 기록되는 값은 동일해야 함
  - 3은 아니더라도, 특정 상수는 동일해야 함

$$
X \in R^{n_H^{[I]} \times n_H^{[I]} \times 3}
$$
$$
K^{[1]} \in R^{f^{[1]} \times f^{[1]} \times 3}
$$
$$
b^{[1]} \in R
$$
$$
A^{[1]} \in R^{n_H^{[I]} \times n_H^{[I]} }
$$
- 최종적으로 하나의 scala값이 생성되는 상태
- 여러개의 필터가 있다면

$$
K_{l_I}^{[1]} \in R^{f^{[1]} \times f^{[1]} \times 3}
$$
$$
X \bigotimes K_{l_I}^{[1]} + b_{l_I}^{[1]}, A_{l_I}^{[1]} \in R^{n_H^{[1]} \times n_W^{[1]} } 
$$
- 도출된 $A_1^{[1]}, A_2^{[1]}, ... ,A_{l_I}^{[1]}$ 들이 모여 하나의 General한 Conv Layer가 생성됨
- 여러개의 채널, 그리고 여러개의 filter에 따른 변화 확인
- 다음 Conv Layer를 구하기 위해서는,
  - $A^{[1]}$에 $K^{[2]}$라는 커널 생성 이후 $A^{[2]}$를 생성
- 채널(Kernel)에 따라, 다음 Layer의 **이미지 수**가 결정됨($l_I$)
  - $K^{[2]} \in R^{f^{[2]} \times f^{[2]} \times l_1 \times l_2}$
  - 차차 쌓여가는 형태로 구성됨
  - $l_2$의 수에 따라 $A^{[2]}$가 결정됨
  - 차원이 증가하는 형태

### Cascaded Conv Layers
- 입력
  - $X  \in R^{n_H^{[I]} \times n_W^{[I]} \times l_I}$
- $Conv2D(X; K^{[1]}, \vec{b}^{[1]})$
  - $K^{[1]} \in R^{f^{[1]} \times f^{[1]} \times l_I \times l_1}$
  - $\vec{b}^{[1]} \in R^{l_i}$ 
  - $A^{[1]} \in R^{n_H^{[1]} \times n_W^{[1]} \times l_1}$
  - 관련 사이즈 변경은, 다음 공식을 따름
    - $n_H^{[1]} = n_H^{[I]} - f^{[1]} + 1$
    - $n_W^{[1]} = n_W^{[I]} - f^{[1]} + 1$
- $Conv2D(A^{[1]}; K^{[2]}, \vec{b}^{[2]})$ - 다음 레이어
  - $K^{[2]} \in R^{f^{[2]} \times f^{[2]} \times l_I \times l_2}$
    - $n_H^{[2]} = n_H^{[1]} - f^{[2]} + 1$
    - $n_W^{[2]} = n_W^{[1]} - f^{[2]} + 1$
  - $A^{[2]} \in R^{n_H^{[2]} \times n_W^{[2]} \times l_2}$

### Minibatch in Conv Layers
- Cascaded 방식과 유사하나, 여러 배치가 동작하는 형태이므로, `N`차원이 붙음
- $K$와 $\vec{b}$의 변경사항은 없음
- 입력
  - $X  \in R^{N \times n_H^{[I]} \times n_W^{[I]} \times l_I}$
- $Conv2D(X; K^{[1]}, \vec{b}^{[1]})$
  - $K^{[1]} \in R^{f^{[1]} \times f^{[1]} \times l_I \times l_1}$
  - $\vec{b}^{[1]} \in R^{l_i}$
  - $A^{[1]} \in R^{N \times n_H^{[1]} \times n_W^{[1]} \times l_1}$
- $Conv2D(A^{[1]}; K^{[2]}, \vec{b}^{[2]})$ - 다음 레이어
  - $K^{[2]} \in R^{f^{[2]} \times f^{[2]} \times l_I \times l_2}$
    - $n_H^{[2]} = n_H^{[1]} - f^{[2]} + 1$
    - $n_W^{[2]} = n_W^{[1]} - f^{[2]} + 1$
  - $A^{[2]} \in R^{N \times n_H^{[2]} \times n_W^{[2]} \times l_2}$
