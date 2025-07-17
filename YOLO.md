# YOLOv8 vs YOLOv11 비교 정리

> 본 문서는 YOLOv8과 YOLOv11의 주요 특징, 차이점, 개선 사항을 정리한 내용입니다. 모델 선택 시 참고용으로 활용 가능합니다.

---

## 📌 개요

| 항목       | YOLOv8                        | YOLOv11 (예정 또는 커뮤니티 버전)           |
|------------|-------------------------------|---------------------------------------------|
| 개발자     | Ultralytics                   | 오픈소스 커뮤니티 또는 일부 논문 기반 버전 |
| 발표 시기  | 2023년 1월                    | 2024년 후반 ~ 2025년 예상                   |
| 기반 구조  | YOLO Series, PyTorch          | 대부분 PyTorch 기반, 구조는 다양            |

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

## 🚀 YOLOv11 특징 (예상/비공식)

> 아직 공식 릴리스는 없으나, 커뮤니티나 논문 기반의 예상 내용을 바탕으로 정리했습니다.

- 일부 구현은 **RepVGG, RT-DETR 구조**를 도입
- **Attention 메커니즘** 개선 가능성 (ex: Efficient Attention, Swin 기반 등)
- 기존 YOLOv8 대비 **더 깊은 네트워크**와 **정확도 향상** 추구
- NAS(Neural Architecture Search)를 통한 자동 설계 구조 실험
- 일부는 **RTMDet, YOLO-World** 등 다른 최신 모델과 통합되기도 함

---

## 🔍 v8 vs v11 주요 차이점

| 항목           | YOLOv8                           | YOLOv11 (예상)                          |
|----------------|----------------------------------|------------------------------------------|
| 구조 방식       | Anchor-Free, CNN 중심            | CNN + Attention 또는 Transformer Hybrid |
| 성능 최적화     | 실용성 중시, 속도-정확도 균형    | 정확도 위주, 복잡성 증가 가능성         |
| 경량화 옵션     | 있음 (v8n, v8s 등)               | 추후 경량 버전 가능성 있음               |
| 활용 범위       | 탐지, 세그먼트, 분류 등 통합 설계 | 구조마다 다름 (통합성은 낮음)           |
| 배포 용이성     | `ultralytics` 패키지로 쉬움       | 직접 커스터마이징 필요 가능성 큼         |

---

## 📈 개선점 요약

| 개선 항목       | YOLOv8 → YOLOv11 예상 개선 사항      |
|----------------|----------------------------------------|
| Accuracy       | 더욱 정밀한 객체 구분 (작은 객체 등)    |
| Backbone       | 기존보다 더 깊거나 고급 구조 가능 (ex: CSP → RepVGG) |
| Feature Fusion | FPN → BiFPN, PAN 등 더 효과적 연결 구조 |
| 활용 확장성     | 포즈 추정, 텍스트 감지까지 확장 가능     |

---

## 📚 참고 링크

- [YOLOv8 공식 문서](https://docs.ultralytics.com/)
- [YOLO GitHub](https://github.com/ultralytics/ultralytics)
- [YOLOv9~11 관련 실험 GitHub](https://github.com/WongKinYiu)

> ※ YOLOv11은 아직 공식 릴리스된 버전이 아니므로 일부 내용은 추정에 기반합니다.

---

## 📌 정리

- YOLOv8은 현재까지 가장 널리 사용되는 안정적인 버전입니다.
- YOLOv11은 향후 더 높은 정확도와 향상된 구조로 출시될 가능성이 있으며, 일부 커뮤니티에서 실험 중입니다.
- 목적과 환경에 맞춰 YOLOv8을 먼저 활용하고, 추후 YOLOv11 성능을 비교 적용하는 전략을 추천드립니다.


