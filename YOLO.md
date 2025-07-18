# YOLO버전 별 비교 정리
---

## 🧠 YOLO란?

**YOLO(You Only Look Once)**는 실시간 객체 탐지(Object Detection)를 위한 딥러닝 알고리즘입니다.  
한 번의 신경망 연산(Forward Pass)으로 **이미지 속 객체의 위치(Bounding Box)**와 **종류(Class)**를 동시에 예측합니다.

### 🔍 YOLO의 핵심 특징

- 이미지 전체를 한 번에 처리 → **매우 빠름 (real-time)**
- 다양한 객체를 동시에 탐지 가능 (예: 사람, 자동차, 강아지 등)
- YOLOv1부터 v11까지 지속적으로 발전 중

### 📦 YOLO의 주요 활용 분야

- 자율주행 차량 (보행자, 차선 탐지)
- CCTV 기반 보안 시스템
- 산업 자동화 및 결함 검사
- 스포츠 분석, 드론 추적, 헬스케어 등


## 🧠 YOLOv8 vs YOLOv11 vs YOLOv12 비교
| 항목     | YOLOv8                | YOLOv11                        | YOLOv12                    |
| ------ | --------------------- | ------------------------------ | -------------------------- |
| 릴리즈 시기 | 2023.01               | 2024.03                        | 2025.02                |
| 프레임워크  | PyTorch + Ultralytics | PyTorch (확장 구조, 커뮤니티 기반)       | PyTorch + Ultralytics (공식) |
| 주요 구조  | Anchor-Free, CNN      | RepVGG, Attention, Transformer | Improved TaskHead, Loss 개선 |
---

## ✅ YOLOv8 특징

- **Anchor-Free 구조** 도입  
- **모듈형 설계** (Detection / Segmentation / Classification 통합 가능)  
- **ONNX, TensorRT 등 내보내기 쉬움**  
- **`ultralytics` 패키지로 손쉬운 사용**  
- **`task=detect/segment/classify/pose` 등 직관적**  
- 높은 정확도 대비 속도 균형 우수  

### 성능 (COCO 기준, v8n ~ v8x)

| 모델 | mAP50-95 | FPS (Tesla T4 기준) |
|------|----------|----------------------|
| v8n  | 37.3     | 100+ FPS             |
| v8m  | 46.7     | ~50 FPS              |
| v8x  | 53.0     | ~30 FPS              |

---
## ✅ YOLOv11 특징 
- 일부 구현은 **RepVGG, RT-DETR 구조**를 도입
- **Attention 메커니즘** 개선 가능성 (ex: Efficient Attention, Swin 기반 등)
- 기존 YOLOv8 대비 **더 깊은 네트워크**와 **정확도 향상** 추구
- NAS(Neural Architecture Search)를 통한 자동 설계 구조 실험
- 일부는 **RTMDet, YOLO-World** 등 다른 최신 모델과 통합되기도 함

## ✅ YOLOv12 특징
- TaskAlignedAssigner를 기본 활성화 → 정확도 향상
- LossHead 구조 변경 → 학습 안정성 향상
- scale_loss 동적 계산 도입 (클래스 불균형 개선)
- iou_type 선택 가능 (ciou, diou 등)
- resume 옵션으로 학습 이어하기 개선
- Ultralytics 패키지에서 그대로 사용 가능 (v8과 거의 호환)
---

## 🔍 버전별 성능 및 차이점 정리
| 항목          | YOLOv8                | YOLOv11                  | YOLOv12                      |
| ----------- | --------------------- | -------------------------- | ---------------------------- |
| 구조 복잡도      | 비교적 간단                | 중간\~복잡 (RepVGG, Attention) | 정리된 구조, 성능·학습 균형             |
| 정확도(mAP) 향상 | 기본 기준                 | 소폭 향상 (실험에 따라 다름)          | **공식 기준 약 1\~2% 향상** (v8 대비) |
| 학습 안정성      | 보통                    | 실험 구조에 따라 차이 큼             | **상당히 향상 (새로운 LossHead)**      |
| 클래스 불균형 대응  | 없음                    | 없음                         | **`scale_loss=True` 기본 적용**  |
| 배포 용이성      | 매우 쉬움 (`ultralytics`)  | 매우 쉬움 (`ultralytics`) | 매우 쉬움 (`ultralytics`) |                                                                 |


---

## 📈 YOLOv12에서 개선된 주요 기술
| 개선 요소                 | 설명                                       |
| --------------------- | ---------------------------------------- |
| `TaskAlignedAssigner` | 예측-정답 정렬을 더 정확하게 개선해 detection 성능 향상     |
| `scale_loss`          | 클래스 불균형 대응을 위해 손실 비율을 자동 조절              |
| `LossHead` 구조 변경      | IoU loss와 classification loss 분리로 학습 안정화 |
| 다양한 IoU 선택 가능         | `ciou`, `diou`, `giou` 등 사용자가 지정 가능      |
| 학습 resume 기능 강화       | 학습 재시작 시 더욱 안정적이고 정확하게 이어짐               |

---
## 📦 YOLO와 다른 알고리즘 비교 
| 모델           | 특징                 | YOLO와 차이점           |
| ------------ | ------------------ | ------------------- |
| Faster R-CNN | 2단계 탐지, 정확도 높음     | 속도가 느림              |
| SSD          | 실시간 가능, YOLO보다 가벼움 | 정확도는 YOLO보다 낮을 수 있음 |
| RT-DETR      | 트랜스포머 기반 탐지        | 매우 정확하지만 무거움        |


## 📚 참고 링크

- [YOLOv8 공식 문서](https://docs.ultralytics.com/)
- [YOLO GitHub](https://github.com/ultralytics/ultralytics)
- [YOLOv9~11 관련 실험 GitHub](https://github.com/WongKinYiu)
  




