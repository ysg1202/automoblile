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
[컨볼루션연산](https://claude.ai/public/artifacts/2c09bc56-7cc3-4ea0-b3ca-7678aa107756)

## 필터종류
### 블러필터






