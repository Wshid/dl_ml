## CH06_01. (이론강의) Pooling Layers

### Max/Average Pooling
- Window에서는
  - Kernel + bias -> activation -> a를 얻는 과정
- 유사함
- 두가지 방법 존재
  - Max Pooling
    - $W -> \phi = max(W) -> \phi$
  - Average Pooling
    - $W -> \phi = \frac{1}{||W||}\sum_{x \in W} x -> \phi$
  - Activation을 따로 통과하지 않음
- Window를 뽑고 pooling 하고를 반복
- `f`는 filter size를 의미

#### 1차원 pooling
$$
W_0 = \begin{matrix}(x0 & x1 & x2) \end{matrix} \rightarrow \phi_0 = max(W_0) -> \phi_0
$$
$$
W_1 = \begin{matrix}(x1 & x2 & x3) \end{matrix} \rightarrow \phi_1 = max(W_1) -> \phi_1
$$
- shape 계산 방법도 이전과 동일
  - $n_H = n_H - f + 1$

#### 2차원 Pooling
- pooling을 하면, 그만큼 차원이 낮아짐
- 입력 matrix X에서 Window 선정 이후, pooling 하는 예시

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
\phi[0,0] = max(W_{0,0})
$$

$$
W_{0,1} = X[0:3, 1:4] = \begin{pmatrix}
X[0,1] & X[0,2] & X[0,3] \\
X[1,1] & X[1,2] & X[1,3] \\
X[2,1] & X[2,2] & X[2,3] \\
\end{pmatrix}
$$
$$
\phi[1,0] = max(W_{1,0})
$$

- 연산을 모두 마친 형태(window보다 한 차원이 줄어듦)

$$
\phi = \begin{pmatrix}
  \phi[0,0] & \phi[0,1] \\
  \phi[1,0] & \phi[1,1]
\end{pmatrix}
$$

- pooling은 이미지별로 channel-wise가 아니라
  - 이미지별 pooling을 의미함

### Padding
- 주변에 0값을 채워주는 형태
  - zero-padding
- 하는 이유
  - corner case에 대한 대응이 가능함
  - 특정 값이 중앙에 있을때의 검증 등
  - input, output size가 동일하게 변경됨
- $n'_H = n_H + 2p - f + 1$
  - 원본 이미지 사이즈가 변경됨
- 아래 식을 만족했을때, output shape이 변경되지 않음
  - $\frac{f-1}{2} = p$

$$
X = \begin{pmatrix}
0 & 0 & 0 & 0 & 0 & 0 \\
0 & X[0,0] & X[0,1] & X[0,2] & X[0,3] & 0 \\
0 & X[1,0] & X[1,1] & X[1,2] & X[1,3] & 0 \\
0 & X[2,0] & X[2,1] & X[2,2] & X[2,3] & 0 \\
0 & X[3,0] & X[3,1] & X[3,2] & X[3,3] & 0 \\
0 & 0 & 0 & 0 & 0 & 0 \\
\end{pmatrix}
$$

### Strides
- 윈도우를 순차적으로 판단하지 않고, 건너뛰는 형태
- $W_{i,j} = X[i:i+(f-1), j:j+(f-1)]$
  - $0 \le i \le n_H -f, i = i' \cdot s, i' \in W $
    - $i$는 col number
  - $0 \le j \le n_H -f, i = j' \cdot s, j' \in W $
- 가우스 함수(내림)
  - $n'_H = [\frac{n_H-f}{s} + 1]$

### I/O Shapes
- Conv와 Pooling Layer에 모두 적용 가능한 공식
- $n'_H = [\frac{n_H+2p-f}{s} + 1]$
