# 📚 Convolutional Neural Network (CNN)

## 🧠 개념

**CNN(합성곱 신경망)**은 이미지나 시계열 데이터와 같은 **공간적 구조**를 가진 데이터를 처리하기에 최적화된 **딥러닝 모델**입니다.  
주로 이미지 인식, 영상 처리, 자연어 처리, 음성 인식 등에 사용됩니다.

---

## 🧩 주요 구조

1. **Convolution Layer (합성곱 계층)**  
   - 이미지에서 **특징(Feature)**을 추출  
   - 필터(커널)를 사용해 입력 이미지와 **합성곱 연산** 수행

2. **Activation Function (활성화 함수)**  
   - 비선형성 부여 (주로 ReLU 사용)  
   - `f(x) = max(0, x)`

3. **Pooling Layer (풀링 계층)**  
   - 공간 정보를 압축하여 연산량 감소  
   - **Max Pooling** 또는 **Average Pooling** 사용

4. **Fully Connected Layer (완전 연결 계층)**  
   - 최종 분류 또는 회귀를 위한 출력  
   - 기존 MLP(다층 퍼셉트론)와 유사
5. **Output Layer**
   - Softmax 등으로 최종 결과 출력      

---

## 📘 자주 등장하는 용어

| 용어 | 설명 |
|------|------|
| **Filter (Kernel)** | 입력 이미지에서 특징을 추출하는 작은 가중치 행렬 |
| **Stride** | 필터가 이동하는 간격 |
| **Padding** | 가장자리에 0을 추가하여 출력 크기 조절 |
| **Feature Map** | 필터 연산 결과로 생성된 출력 값 |
| **ReLU (Rectified Linear Unit)** | 비선형 활성화 함수, 음수를 0으로 만듦 |
| **Dropout** | 과적합 방지를 위해 일부 뉴런을 무작위 제거 |
| **Batch Normalization** | 학습 안정성과 속도 향상을 위한 정규화 기법 |

---

## 🧮 대표 CNN 알고리즘 예시

| 모델명 | 특징 |
|--------|------|
| **LeNet-5 (1998)** | 손글씨 숫자 인식용 CNN의 시초 |
| **AlexNet (2012)** | 이미지넷 대회 우승, ReLU & GPU 사용 |
| **VGGNet (2014)** | 3×3 필터만 사용, 깊은 구조 |
| **GoogLeNet (Inception, 2014)** | 다양한 크기의 필터를 병렬 적용 |
| **ResNet (2015)** | **Residual Connection**으로 딥러닝 구조 매우 깊게 가능 |
| **EfficientNet (2019)** | 계산 효율성과 정확도를 모두 개선 |

---

## 📐 기본 구조 요약

```text
입력 (Input) → 합성곱 (Conv) → 활성화 (ReLU) → 풀링 (Pooling) → ...
       → 완전연결층 (Fully Connected) → 출력 (Output)
```

## ⚙️ CNN 하이퍼파라미터 튜닝 요소

| 하이퍼파라미터       | 설명                                                                 | 일반적인 값 예시         | 튜닝 팁 |
|----------------------|----------------------------------------------------------------------|---------------------------|---------|
| **Learning Rate**    | 가중치를 얼마나 빠르게 업데이트할지 결정하는 값                     | 0.1, 0.01, 0.001          | 너무 크면 발산, 너무 작으면 학습 느림 |
| **Batch Size**       | 한 번에 네트워크에 입력되는 샘플 수                                 | 16, 32, 64, 128           | 메모리 상황에 따라 조절 |
| **Epochs**           | 전체 데이터를 몇 번 반복해서 학습할지 결정                          | 10~100 이상               | Early Stopping 고려 |
| **Optimizer**        | 가중치 갱신 방식                                                     | SGD, Adam, RMSprop        | 대부분 Adam부터 시도 |
| **Kernel Size**      | 필터의 크기 (Convolution 연산 범위)                                 | 3x3, 5x5                  | 보통 3x3이 기본 |
| **Stride**           | 필터가 한 번에 이동하는 간격                                        | 1, 2                      | 큰 값일수록 출력 크기 작아짐 |
| **Padding**          | 입력의 경계에 0을 추가하여 출력 크기 조정                           | same, valid, 1, 2         | 보통 'same' 또는 1 |
| **Number of Filters**| 각 합성곱 계층에서 사용하는 필터 수                                 | 16, 32, 64, 128 이상      | 깊은 네트워크일수록 증가 |
| **Activation**       | 비선형성 부여 함수                                                   | ReLU, LeakyReLU, ELU      | 기본은 ReLU |
| **Pooling Size**     | Pooling 층에서 적용할 윈도우 크기                                   | 2x2                       | 보통 2x2, stride=2 |
| **Dropout Rate**     | 일부 뉴런을 무작위로 제거하여 과적합 방지                           | 0.3, 0.5                  | FC 층에 주로 사용 |
| **Weight Initialization** | 초기 가중치 분포 방식                                          | Xavier, He, Normal        | 활성화 함수에 따라 선택 |

---

## CNN의 전체적인 네트워크 구조
<img width="640" height="229" alt="image (1)" src="https://github.com/user-attachments/assets/93a051a6-8655-44d0-a6d4-9ff22e37f067" />

## 컨볼루션연산 예시
- [컨볼루션연산](https://claude.ai/public/artifacts/2c09bc56-7cc3-4ea0-b3ca-7678aa107756)
- [컨볼루션연산 파이프라인_1](https://claude.ai/public/artifacts/df7a5986-dd0a-4a16-af85-ad90959de392)
- [컨볼루션연산 파이프라인_2](https://claude.ai/public/artifacts/a3bda456-4c3f-4127-a921-21ad4c351c98)

## 필터종류
### 블러필터
<img width="171" height="161" alt="블러필터" src="https://github.com/user-attachments/assets/863ad786-c762-4e2b-b49b-b8604b49c9da" />

### 샤프닝필터
<img width="168" height="168" alt="샤프닝필터" src="https://github.com/user-attachments/assets/ca31c06d-e3c7-4fb1-be12-18ab2502e1a8" />

### 수직필터
<img width="167" height="166" alt="수직엣지" src="https://github.com/user-attachments/assets/50962858-6371-4ea2-b1ec-033430cd57cf" />

### 수평필터
<img width="166" height="166" alt="수평엣지" src="https://github.com/user-attachments/assets/8dbd6f2e-5499-410b-ad7d-bdd7c7705b09" />

## ✅ 필터 종류별 요약 비교

| 필터 종류         | 목적               | 특징                           |
|------------------|--------------------|--------------------------------|
| **블러 필터**     | 부드럽게 만들기    | 노이즈 제거, 흐림 효과         |
| **샤프닝 필터**   | 선명하게 만들기    | 경계 강조, 디테일 강화         |
| **수직 엣지 필터**| 세로 방향 경계 감지| 왼쪽↔오른쪽 밝기 차이 탐지     |
| **수평 엣지 필터**| 가로 방향 경계 감지| 위쪽↕아래쪽 밝기 차이 탐지     |

## CNN처리결과
<img width="832" height="691" alt="CNN 처리결과" src="https://github.com/user-attachments/assets/45aae41b-1d22-4ac1-ba31-87c6f5c8b393" />

1. 🟦 수직 엣지 감지 결과
- 오른쪽-왼쪽 밝기 차이를 감지 → 세로선/수직 경계 강조
- 음수: 왼쪽이 밝고 오른쪽이 어두움
- 양수: 왼쪽이 어둡고 오른쪽이 밝음
- 예: -179, -100 → 강한 수직 엣지 존재

2. 🟨 수평 엣지 감지 결과
- 위-아래 밝기 차이 감지 → 가로선/수평 경계 강조
- 예: -248, -156 → 위쪽이 밝고 아래가 어두운 강한 수평 엣지

3. 🟪 블러 처리 결과
- 주변 9개 픽셀의 평균값으로 중앙 픽셀을 대체 → 부드럽고 흐림 효과
- 예: 147, 129, 102 → 원래보다 경계가 흐릿해짐

4. 🟥 샤프닝(Sharpening) 처리 결과
- 중앙 픽셀 강조 + 주변 억제 → 윤곽, 경계 강화
- 예: 348, -227, 337 → 밝기 대비가 강하게 나타나는 영역 강조됨

## CNN 파이프라인
### 1. 컬러 이미지의 RGB 분해
- 각 채널은 별도의 행렬로 처리됨 (3개의 2D 배열)
- CNN이 이미지를 처리할 때는 이미지의 각 색상 채널을 분리해서 처리
- 각 채널별로 필터 적용 후 특징 추출
<img width="1215" height="637" alt="1  채널 분리" src="https://github.com/user-attachments/assets/1b3f368a-7686-4603-9457-f71262c452a0" />

### 2. 패딩적용
<img width="1126" height="626" alt="2  패딩 적용" src="https://github.com/user-attachments/assets/a9ded569-c909-4a31-ba4c-340bfbd4dcc4" />

### 3. 컨볼루션 연산
<img width="1381" height="466" alt="3  컨볼루션 연산" src="https://github.com/user-attachments/assets/3864954c-baf8-44a6-9796-4be0f030dbfe" />

### 4. ReLU 적용
<img width="1367" height="645" alt="4  ReLU 적용 " src="https://github.com/user-attachments/assets/cf3bfcf4-8f01-4b3c-8d30-6092700d053b" />

### 5. 피쳐맵 생성
<img width="1377" height="501" alt="5  피쳐맵 생성 완료 " src="https://github.com/user-attachments/assets/2de21d43-99de-44bd-bc02-8e185a5782b5" />

## 각 피쳐맵의 처리결과 
<img width="1185" height="832" alt="7  각 필터별 결과2 " src="https://github.com/user-attachments/assets/cc5cf4fa-1e2b-4867-9489-9ffd5a4337e5" />

### 필터 적용 결과
| 필터 종류        | 결과 요약                          | 의미 및 해석                            |
| ------------ | ------------------------------ | ---------------------------------- |
| **원본 입력**    | 5×5 영역 모두 거의 동일한 값 (e.g., 127) | 변화가 거의 없는 평탄한 표면                   |
| **수직 엣지 감지** | 작은 숫자(0\~6)만 일부 존재             | 수직 방향 밝기 변화가 **거의 없음**             |
| **수평 엣지 감지** | 약한 수치 (e.g., 5, -1, 0 등)       | 수평 방향으로도 **밝기 변화 거의 없음**           |
| **블러 처리**    | 대부분 126\~127                   | 거의 동일한 값을 평균 → 더 부드러워짐             |
| **샤프닝 처리**   | 약간 변화 (e.g., 114\~131)         | 중심 픽셀 강조하지만 **뚜렷한 경계가 없으므로 효과 적음** |

### 시각화 결과
| 처리        | 120×120 확대 이미지 | 해석                     |
| --------- | -------------- | ---------------------- |
| **수직 엣지** | 거의 **검정**      | 엣지 없음 (0 또는 매우 작은 값)   |
| **수평 엣지** | 거의 **검정**      | 수평 경계도 없음              |
| **블러**    | 부드러운 회색        | 더 균일한 이미지로 변환됨         |
| **샤프닝**   | 약한 대비 변화       | 경계가 거의 없어, 샤프닝 효과도 제한적 |

### 결론
이 영역은 밝기 변화가 거의 없는 평탄한 붉은색 표면이기 때문에 엣지 감지 필터는 거의 0에 가까운 출력을 내고 블러와 샤프닝은 거의 변화 없는 결과를 보여준다.





