## CH07_01. (이론강의) Convolutional Neural Networks

### Modules of Classifier
- 컴퓨터 비전 내의 개념
  - Input image를 그대로 사용하면 성능이 떨어지니,
    - 컴퓨터가 인식할 수 있을 정도로 feature 변환
- 순서
  - X(Input)
  - **Feature Extractor**
    - Convolutional Layers + (pooling layer)
    - Feature Vector 반환
  - **Classifier**
    - Dense Layers(Convolutional Layer의 flatten)
    - Class Scores 반환4
- 좋은 feature를 만드는 알고리즘?
  - e.g. 강아지를 넣으면, 강아지 형상의 feature들이 군집화 되고,
    - 고양이를 넣으면 고양이 형상의 feature들 군집화
- feature를 만드는 알고리즘은 매우 많음

### Convolutional Neural Networks
>$\uparrow J \in R$
>$L_{CE}$
>$\uparrow(\hat{Y})^T \in R^{N \times K}$
>$L_{Softmax}$
>$\uparrow(Z^{[5]})^T \in R^{N \times l_5}$
>$L_{Dense}^{[5]} \vec{b}^{[5]} \in R^{l_5}, W^{[5]} \in R^{l_4 \times l_5}$
>$\uparrow(A^{[4]})^T \in R^{N \times l_4}$
>$L_{Dense}^{[4]}, \vec{b}^{[4]} \in R^{l_4}, W^{[4]} \in R^{n_H^{2} \cdot n_W^{2} \cdot l_2 \times l_4}$
>$\uparrow (A^{[3]})^T \in R^{N \times N_H^{[2]} \times N_W^{[2]} \times l_2}$
>$L_{Flatten}^{[3]}$
>$\uparrow A^{[2]} \in R^{N \times N_H^{[2]} \times N_W^{[2]} \times l_2}$
>$L_{Conv2D}^{[2]}, \vec{b}^{[2]} \in R^{l_2}, K^{[2]} \in R^{f^{[2]} \times f^{[2]} \times l_1 \times l_2}$
>$\uparrow A^{[1]} \in R^{N \times N_H^{[1]} \times N_W^{[1]} \times l_1}$
>$L_{Conv2D}^{[1]}, \vec{b}^{[1]} \in R^{l_1}, K^{[1]} \in R^{f^{[1]} \times f^{[1]} \times l_I \times l_1}$
>$\uparrow$
>$X \in R^{N \times N_H^{[I]} \times N_W^{[I]} \times l_I}$
- Feature Extractor
  - $L^{[1]}$ ~ $L^{[3]}$
- Classifier
  - $L^{[4]}$ ~ $L_{Softmax}$
- Loss Calculator
  - $L_{CE}$
- 레이어를 쌓으면 쌓을수록 파라미터가 많아짐
- Feature Extractor의 예시
  - HOG, SIFT, FAST
  - 하지만 DL이 되면서, FE도 이런 변수를 학습하는 대상이 됨

### LeNet
- Feature Extractor, Classifier만 존재
  - ![image](https://user-images.githubusercontent.com/10006290/226153519-4e071656-b4a6-414b-b874-f0490127bf22.png)
- 테이블 생성 필요
  - ![image](https://user-images.githubusercontent.com/10006290/226153477-8f210a8d-887c-4df1-810b-68778ffec7b2.png)
