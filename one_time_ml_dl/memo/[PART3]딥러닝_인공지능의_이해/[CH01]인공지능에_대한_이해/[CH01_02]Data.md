## CH01_02. Data

### Data
- Training set, Validation set, Test set
- Training -> Tuning(Validation) -> Test
- **Training/Tuning이 끝날때까지 Test set을 사용하면 X**
  - Test set의 결과를 사용한 순간, 이 역시 validation set이 됨
- Test는 Training/Tuning에 없는 데이터로 구성해야 함

### 수집 특징
- 어떤 문제를 풀 것이냐에 따라 구분지어 모아야 함
- Classification, Semantic Segmentation, Detection, Pose Estimation, Visual QnA

### Data is Important
- 데이터가 많으면 많을수록, 정확도는 높아짐
  - 기울기는 줄 수 있어도

### Data is Expensive
- 구분이 디테일해질수록
- 데이터 자체가 전문화 되어 있을 경우(e.g. 병원 진료 데이터)

### Active Learning
- Unlabled pool에서 influence한 데이터를 먼저 선별하여
- 먼저 데이터 생성 요청(labeling)
- 이후 labeled된 데이터를 training에 사용

### Good Data vs Bad Data
- Bias X
  - 데이터가 한쪽으로 치우쳐지지 않아야함
  - 보지 않은 데이터(Test set)에서도 강하려면
    - 편향적이지 않은 데이터가 필요
- Label이 모두 정확하지 않을 수 있음
  - e.g. 같은 의사들이 보기에도 의견이 다름
  - e.g. 사진에서 박스를 치는 작업을 할 때도 사람마다 작업 결과가 다를 수 있음

### Data Centric AI
- **Model-Centric AI**
  - hyper-parameter를 튜닝하는 입장
- **Data-Centric AI**
  - 데이터가 중요함
  - 데이터를 튜닝해서 더 잘되게 하는 방법

### Data-Centric AI
- 양을 늘리는 것 뿐 아니라
- 데이터의 질을 높이는게 필요
  - 노이즈 줄이기
