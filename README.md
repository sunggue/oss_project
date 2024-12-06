#   How Old Are You? Age Prediction Through CNN

## Introduce
CNN(Convolutional Neural Network)+MLP(Multi-Layer Perceptron) 구조를 결합하여 주어진 이미지 속 인물의 나이를 예측합니다.

---
## Dataset Description
- **UTKFace Dataset**은 약 23,000개의 얼굴 이미지로 구성되어 있으며, 각 이미지에는 나이, 성별, 인종에 대한 레이블이 포함되어 있습니다.
![UTKface](<assets/UTKface.jpg>)

---

## Code Description

### `dataset.ipynb`
- 주어진 경로에 있는 데이터셋을 로드합니다.  
- 로드된 이미지를 전처리합니다. *(4차원 배열 + Min-Max scaling)*  
- 나이에 따른 이미지 수를 시각화합니다.  
![Dataset Visualization](<assets/Dataset Visualization.jpg>)  

### `model.ipynb`
- **CNN**으로 특성을 추출하고 **MLP**로 회귀하는 구조의 모델을 구축합니다.  
![Model Architecture](<assets/Model Architecture.jpg>)   
- 이미지의 복잡한 패턴을 학습하기 위해 **ReLU** 활성화 함수를 사용했습니다.  
- MLP 구조에서 **Dropout**을 구현하여 **과적합**을 방지했습니다.  
- 회귀 문제이기 때문에 손실 함수로 **Mean Squared Error**를 채택했습니다.  
- 성능 평가는 직관적인 확인을 위해 **Mean Absolute Error**를 채택했습니다.  
- 모델을 학습시키고, **Epoch**에 따른 **Mean Absolute Error**를 출력합니다.  
![Training Performance](<assets/Training Performance.jpg>)   

### `face_detector.ipynb`
- `cv2.CascadeClassifier`를 이용하여 이미지 중 얼굴 부분만을 추출합니다.  
- 원본 이미지와 추출된 얼굴 이미지를 시각화합니다.  
![Face Detection](<assets/Face Detection.jpg>) 
- 추출한 얼굴 이미지를 전처리합니다. *(4차원 배열 + Min-Max scaling)*  

---

## How to Use
1. [데이터셋 링크](<https://www.kaggle.com/datasets/jangedoo/utkface-new>)에서 데이터셋을 다운받아 **UTKface** 폴더 안에 넣습니다.    
2. 나이를 확인하고 싶은 인물의 이미지를 **input** 폴더 안에 넣습니다.  
3. `main.ipynb`에서 이미지의 이름을 작성하고 코드를 실행하여 결과를 확인합니다.  
![Image Name](<assets/Image Name.jpg>)  
![Result Example](<assets/Result Example.jpg>) 

---

## Limitations
- 나이에 따른 이미지 수를 분석한 결과, **0~5세**와 **20~30세**의 이미지가 다른 나이대에 비해 확연히 많으며, 나이대가 올라갈수록 이미지 수가 줄어드는 경향이 있습니다. 이러한 데이터 불균형으로 인해 **0~5세**와 **20~30세** 이미지에서는 높은 정확도를 보이지만, 다른 나이대에서는 낮은 정확도를 확인할 수 있었습니다.  
- **절대적인 이미지 수**를 늘리거나, **사전에 학습된 딥러닝 모델**을 사용하면 더 나은 결과를 얻을 수 있을 것으로 예상됩니다.
