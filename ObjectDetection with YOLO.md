# YOLOv8 학습 전체 흐름 정리
---

## ✅ 1. 환경 설정

### 필수 요소
- Python 3.8 이상
- PyTorch
- CUDA (GPU 사용 시)
- `ultralytics` 라이브러리 설치

### 설치 방법
```bash
pip install ultralytics
```

---

## ✅ 2. 데이터셋 준비

### 1) 데이터 구조 (YOLO 포맷)
```
datasets/
├── images/
│   ├── train/
│   └── val/
├── labels/
│   ├── train/
│   └── val/
```

### 2) 라벨 형식 (YOLO TXT)
```
<class_id> <x_center> <y_center> <width> <height>
(모두 0~1 사이 비율로 표시)
```

### 3) 클래스 정의
```yaml
# data.yaml 예시
path: ./datasets
train: images/train
val: images/val

nc: 2
names: ['lane', 'traffic_sign']
```

---

## ✅ 3. 학습 설정 및 실행

YOLOv8에서는 Python 코드 또는 CLI(Command Line Interface)로 학습 가능

### CLI 명령어 예시
```bash
yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=100 imgsz=640
```

### 주요 파라미터
- `task`: detect / segment / classify 중 선택
- `mode`: train / val / predict / export
- `model`: 사전학습 모델 또는 커스텀 모델
- `data`: 데이터셋 구성 파일
- `epochs`: 학습 반복 수
- `imgsz`: 입력 이미지 크기

---

## ✅ 4. 모델 검증 및 추론

### 검증 (Validation)
```bash
yolo task=detect mode=val model=runs/detect/train/weights/best.pt data=data.yaml
```

### 추론 (Inference)
```bash
yolo task=detect mode=predict model=runs/detect/train/weights/best.pt source=sample.jpg
```

### 결과 저장
- 결과는 `runs/detect/predict` 또는 `runs/detect/train` 디렉터리에 저장됨

---

## ✅ 5. 결과 확인 및 평가

- mAP (mean Average Precision)
- Precision, Recall
- confusion matrix 및 시각화 결과 자동 제공

---

## ✅ 6. 추가 팁

- `augmentation`을 통해 성능 향상 가능
- `export` 기능으로 ONNX, TensorRT 등 다양한 포맷 변환 가능
```bash
yolo mode=export model=best.pt format=onnx
```
- TensorBoard 연동 가능

---

## 🔗 추천 리소스

- [Ultralytics YOLO Docs](https://docs.ultralytics.com/)
- [Roboflow](https://roboflow.com/)
- [Label Studio](https://labelstud.io/)

---

> 📚 YOLOv8 외에도 다양한 AI 모델 학습법은 [GPT온라인](https://gptonline.ai/ko/)에서 확인하세요!
