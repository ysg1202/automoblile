# NVIDIA TAO Toolkit 개요 

## 🧠 NVIDIA TAO Toolkit이란?

**TAO (Train, Adapt, Optimize)** Toolkit은 NVIDIA에서 제공하는 로우코드 기반의 딥러닝 모델 학습 프레임워크입니다. 다음과 같은 기능을 제공합니다:

- 최신 딥러닝 모델 학습 지원  
- NVIDIA의 사전 학습(pre-trained) 모델을 활용한 전이 학습  
- NVIDIA 엣지 디바이스(Jetson, DRIVE 등)용으로 모델 최적화 및 배포

TAO는 특히 **자율주행** 분야에서 효과적으로 활용됩니다.

---

## 🧰 주요 특징

- ✅ 로우코드 CLI 및 Jupyter 노트북 인터페이스 지원  
- ✅ 시각 인식 작업에 적합한 사전 학습 모델 제공  
- ✅ 모델 가지치기(pruning), 양자화(quantization), INT8 최적화 지원  
- ✅ TensorRT, DeepStream, Triton, TAO Deploy로 배포 가능  
- ✅ Jetson, DRIVE AGX, x86 GPU 플랫폼과 호환  

---

## 🚘 자율주행용 사전 학습 모델 목록

### 1. 객체 감지 (Object Detection)

| 모델       | 백본         | 비고               |
|------------|--------------|--------------------|
| YOLOv4     | CSPDarkNet   | 속도와 정확도 우수 |
| SSD        | ResNet, VGG  | 가볍고 빠름        |
| Faster R-CNN | ResNet      | 높은 정확도        |

### 2. 교통 표지판 분류 (Traffic Sign Classification)

| 모델        | 작업     | 비고                              |
|-------------|----------|-----------------------------------|
| ResNet-18   | 분류     | GTSDB 또는 커스텀 데이터셋 지원     |
| EfficientNet| 분류     | 경량성과 정확도의 균형 우수       |

### 3. 차선 인식 (Lane Detection)

| 모델   | 작업                 | 비고                      |
|--------|----------------------|---------------------------|
| ENet   | 의미 분할            | 실시간 감지 가능           |
| UNet   | 의미 분할            | 높은 정확도 (무거움)       |

### 4. 신호등 인식 (Traffic Light Recognition)

| 모델         | 작업           | 비고                       |
|--------------|----------------|----------------------------|
| DetectNet_v2 | 객체 감지      | 빨강/노랑/초록 상태 감지 가능 |
| YOLOv4       | 객체 감지      | 소형 객체에도 적합          |

### 5. 사람 및 차량 감지

| 모델       | 작업        | 비고                    |
|------------|-------------|-------------------------|
| PeopleNet  | 객체 감지   | 보행자 감지에 특화       |
| VehicleNet | 객체 감지   | 다양한 차량 유형 감지 가능 |

---

## ⚙️ TAO 툴킷 사용 워크플로우

1. 데이터셋 준비 (COCO/VOC/KITTI 형식)  
2. TAO CLI 또는 노트북으로 학습  
3. Pruning (모델 크기 줄이기)  
4. INT8 양자화 (속도 개선 및 최적화)  
5. Jetson 또는 DRIVE용으로 export 및 배포  

---

## 📦 지원 배포 플랫폼

- NVIDIA **Jetson** 시리즈 (Nano, Xavier, Orin 등)  
- NVIDIA **DRIVE AGX** (자율주행 전용 플랫폼)  
- **x86 GPU** 데스크탑 (TensorRT, Triton 사용 가능)

---

## 📚 참고 링크

- [NVIDIA TAO Toolkit 공식 문서](https://developer.nvidia.com/tao-toolkit)  
- [NVIDIA NGC 모델 허브](https://ngc.nvidia.com/catalog/models)  
- [DeepStream SDK](https://developer.nvidia.com/deepstream-sdk)

---

> ✨ TAO는 자율주행 시스템에 필요한 딥러닝을 빠르고 쉽게 구현할 수 있도록 도와주는 강력한 도구입니다!

