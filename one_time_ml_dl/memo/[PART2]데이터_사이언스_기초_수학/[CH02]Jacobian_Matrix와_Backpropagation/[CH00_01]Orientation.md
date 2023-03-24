## CH00_01. Orientation
- 수학에 집중

### Previous Lecture
- `Feature Extractor -> Classifier -> Loss Calculator`로 이루어짐
- 목적에 맞도록 w,b가 학습이 되어야 함
  - backpropacation

### Backpropagation
- Neural Netowrk를 학습시키기 위해 사용

### Chain Rule and Backpropagation
- Chain Rule, 합성 함수의 미분
- Chain Rule(기반) -> Backpropagation
- 하나의 입/출력에 대한 미분이 아닌
  - 여러개의 입/출력에 대한 미분이 필요
- 아래 화살표의 **역순으로** backpropagation이 진행됨
  >$\uparrow$
  >$L_{CE}$
  >$\uparrow$
  >$L_{Softmax}$
  >$\uparrow$
  >$L_{Dense}^{[5]}$
  >$\uparrow$
  >$L_{Dense}^{[4]}$
  >$\uparrow$
  >$L_{Flatten}^{[3]}$
  >$\uparrow$
  >$L_{Conv2D}^{[2]}$
  >$\uparrow$
  >$L_{Conv2D}^{[1]}$
  >$\uparrow$
  >$X \in R^{N \times N_H^{[I]} \times N_W^{[I]} \times l_I}$
- $L_{Softmax}$
  - $\frac{\partial J}{\partial W^{[5]}}$, $\frac{\partial J}{\partial \vec{b}^{[5]}}$
- $L_{Dense}^{[5]}$
  - $\frac{\partial J}{\partial W^{[4]}}$, $\frac{\partial J}{\partial \vec{b}^{[4]}}$
- $L_{Flatten}^{[3]}$
  - $\frac{\partial J}{\partial K^{[2]}}$, $\frac{\partial J}{\partial \vec{b}^{[2]}}$
- $L_{Conv2D}^{[2]}$
  - $\frac{\partial J}{\partial K^{[1]}}$, $\frac{\partial J}{\partial \vec{b}^{[1]}}$
- 결과적으로 벡터와 행렬에 대한 **미분**이 필요

### Jacobian Matrices
- 4가지의 미분 방법이 필요함
  - 벡터 X 스칼라
- $f, x$
  - $\frac{\partial f}{\partial x}$
- $f, \vec{x}$
  - $\frac{\partial f}{\partial \vec{x}}$
- $\vec{f}, x$
  - $\frac{\partial \vec{f}}{\partial x}$
- $\vec{f}, \vec{x}$
  - $\frac{\partial \vec{f}}{\partial \vec{x}}$


### Purpose of This Lecture
- Basic principle of learning
  - 딥러닝의 학습 방법
- Basics for advanced techniques
- Improving math abilities