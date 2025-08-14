# SegFormer와 세그멘테이션 기초 개념

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

