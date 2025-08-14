# SegFormer와 segmentation 기초 개념

## 1. 세그멘테이션(Segmentation) 개요
세그멘테이션(Segmentation)은 이미지를 픽셀 단위로 분류하여 객체의 위치와 형태를 구체적으로 파악하는 기술입니다.  
대표적으로 **Semantic Segmentation**, **Instance Segmentation**, **Panoptic Segmentation**이 있습니다.

| 종류 | 설명 | 예시 |
|------|------|------|
| **Semantic Segmentation** | 픽셀 단위로 '클래스(종류)'를 분류. 같은 클래스의 모든 객체를 하나로 취급 | 도로 전체를 'Road', 하늘 전체를 'Sky'로 분류 |
| **Instance Segmentation** | 픽셀 단위로 개별 객체를 구분 | 같은 'Car'라도 각 차량별로 다른 ID 부여 |
| **Panoptic Segmentation** | Semantic + Instance를 결합 | 배경 클래스는 Semantic, 객체 클래스는 Instance 방식 적용 |

---

## 2. Semantic Segmentation
Semantic Segmentation은 이미지의 모든 픽셀을 특정 클래스 중 하나로 분류하는 기법입니다.

- **목표**: '무엇(What)'이 '어디(Where)'에 있는지를 픽셀 단위로 파악
- **특징**
  - 같은 클래스의 객체는 구분하지 않음
  - 자율주행, 위성 이미지 분석, 의료 영상 진단 등에서 사용
- **단점**
  - 동일 클래스의 객체 구분 불가
  - 객체 경계(Edges) 식별이 어려울 수 있음

**예시 이미지**  
- 도로: 회색  
- 차량: 파란색  
- 보행자: 빨간색  
- 하늘: 파란색

---

## 3. YOLO의 Segmentation
YOLO(You Only Look Once)는 원래 객체 탐지(Object Detection) 알고리즘이지만, 최근 버전(YOLOv8 등)에서는 **Instance Segmentation** 기능도 지원합니다.

- **원리**
  - 바운딩 박스(Bounding Box) + 마스크(Mask) 예측
  - 탐지 네트워크에 마스크 분기(Branch)를 추가하여 각 객체의 픽셀 영역 예측
- **장점**
  - 빠른 속도(Real-time 가능)
  - 객체 단위 분리 가능
- **단점**
  - Semantic Segmentation보다 경계선이 매끄럽지 않을 수 있음
  - 매우 작은 객체나 복잡한 형태의 객체는 정확도 저하 가능

**사용 예시**
```bash
yolo segment predict model=yolov8x-seg.pt source=images/

## 4. SegFormer 개요

SegFormer는 **Transformer 기반의 Semantic Segmentation 모델**로, 2021년 NVIDIA에서 발표했습니다.  
기존 CNN 기반 모델의 한계를 극복하고, 전역 정보(Global Context)를 더 잘 활용할 수 있도록 설계되었습니다.

### 4.1 SegFormer 구조 개요도
![SegFormer Architecture](https://raw.githubusercontent.com/NVlabs/SegFormer/main/figures/SegFormer_architecture.png)  
*SegFormer 구조도 (출처: SegFormer 논문)*

### 4.2 구조 설명

SegFormer는 크게 **Hierarchical Transformer Encoder**와 **Lightweight MLP Decoder**로 나눌 수 있습니다.

#### (1) Hierarchical Transformer Encoder
- 여러 해상도의 특징 맵(feature map)을 생성
- 각 단계(stage)에서 Patch Embedding을 수행하여 이미지의 공간 정보를 줄이고, 채널 수를 늘림
- Self-Attention 기법을 사용하여 **전역 정보(Global context)** 를 효율적으로 학습
- CNN처럼 피라미드 구조를 사용하여 작은 객체부터 큰 객체까지 다양한 크기의 특징을 잡아냄

#### (2) Lightweight All-MLP Decoder
- 복잡한 업샘플링(Deconvolution) 대신 MLP(다층 퍼셉트론)만 사용
- Encoder에서 추출된 다단계 특징맵을 각각 업샘플링하여 동일 해상도로 맞춘 후 병합
- 채널 차원에서 결합 후, 최종 픽셀 단위 클래스 예측

---

### 4.3 SegFormer의 장점
1. **심플한 구조**: 복잡한 디코더 불필요 → 모델 크기 작음
2. **정확도 + 속도 균형**: 적은 연산량으로도 높은 mIoU 달성
3. **다양한 크기 지원**: B0~B5까지 다양한 백본 제공
4. **전역+지역 정보 동시 활용**: Transformer의 전역 정보 처리 능력과 CNN의 로컬 특징 결합
5. **모바일 환경 가능**: B0~B2는 모바일/임베디드 환경에서도 동작 가능

---

### 4.4 SegFormer 백본 버전 비교

| 버전 | 파라미터 수(M) | FLOPs(G) | 특징 |
|------|---------------|----------|------|
| **B0** | 3.8M  | 8.4  | 가장 가볍고 빠름 |
| **B1** | 13.7M | 15.9 | 모바일 + 실시간 가능 |
| **B2** | 24.0M | 27.6 | 균형형 |
| **B3** | 44.0M | 62.2 | 더 높은 정확도 |
| **B4** | 60.0M | 121.0 | 대형 모델 |
| **B5** | 81.0M | 182.0 | 가장 높은 정확도, 서버 환경 적합 |

---

## 5. SegFormer vs YOLO Segmentation

| 구분 | SegFormer | YOLO Segmentation |
|------|-----------|-------------------|
| **목적** | Semantic Segmentation | Instance Segmentation |
| **출력** | 픽셀별 클래스 맵 | 객체별 바운딩박스 + 마스크 |
| **속도** | 중간 | 매우 빠름 |
| **정확도** | 복잡한 경계 표현에 강함 | 속도 우선, 경계 표현은 다소 제한 |
| **활용 분야** | 자율주행, 위성, 의료 영상 | 실시간 객체 인식, 로봇 비전 |

---

## 6. 참고 자료
- [SegFormer GitHub](https://github.com/NVlabs/SegFormer)
- [YOLOv8 공식 문서](https://docs.ultralytics.com)
- [SegFormer 논문](https://arxiv.org/abs/2105.15203)
- [Semantic Segmentation 개요](https://paperswithcode.com/task/semantic-segmentation)


