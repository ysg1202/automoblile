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

### 3) yaml 파일 작성 
```yaml
# data.yaml 예시
path: ./datasets
train: images/train
val: images/val

nc: 2
names: ['lane', 'traffic_sign']
```
### 3) 라벨링 과정
#### 클래스 정의
<img width="1213" height="690" alt="클래스 정의 " src="https://github.com/user-attachments/assets/0b623cb7-4479-43a2-9ed8-9a6f5d66503c" />

#### 사각형 박스로 해당 영역 표시
<img width="1136" height="632" alt="사각형으로 라벨링" src="https://github.com/user-attachments/assets/8327c486-d689-45cf-8814-c37317fa620f" />




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

## ✅ 4. 모델 학습 및 추론

### 학습
```python
model.train(
    data="/content/dataset/dataset.yaml",  # yaml 경로
    epochs=120,        # 학습 에폭 수
    imgsz=640,         # 입력 이미지 크기
    batch=16,          # 배치 사이즈
    name="lane_model",  # 저장 폴더 이름
)
```

### 추론 (Inference)
```python
from ultralytics import YOLO

# 모델 로드
model = YOLO('runs/detect/train/weights/best.pt')

# 이미지에 대한 예측
results = model.predict(source='sample.jpg')
```

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

## ✅ 7. 학습결과
### 검증(Validation) 결과
| 클래스         | Precision (P) | Recall (R) | mAP@0.5 | mAP@0.5:0.95 |
|----------------|---------------|------------|---------|---------------|
| 전체 (all)     | 0.609         | 0.485      | 0.477   | 0.193         |
| lane           | 0.529         | 0.414      | 0.430   | 0.142         |
| traffic_sign   | 0.689         | 0.556      | 0.523   | 0.244         |



## 지표 해석
- Precision: 예측한 것 중 정답인 비율 (정확도)
- Recall: 실제 정답 중 예측이 성공한 비율 (재현율)
- mAP@0.5: IoU 0.5 기준에서의 평균 정밀도
- mAP@0.5:0.95: 다양한 IoU(0.5~0.95) 기준의 평균 정밀도 (더 까다로운 성능 지표)

## PR_curve
<img width="2250" height="1500" alt="BoxPR_curve" src="https://github.com/user-attachments/assets/4043be12-eecd-48a3-90cc-6cd6a9dcaa3b" />

## confusion_matrix_normalized
- 행(Row): 실제(정답, Ground Truth) 클래스
- 열(Column): 모델이 예측한(Predicted) 클래스
- 각 칸(Cell): 그 조합에서 예측된 비율 또는 개수
<img width="3000" height="2250" alt="confusion_matrix_normalized" src="https://github.com/user-attachments/assets/334c5e99-0eb7-41d1-982c-e483916b620b" />

### 설명
- lane (실제) → 46%는 맞게 lane, 54%는 background로 잘못 예측
- traffic_sign (실제) → 56%만 맞게 예측, 44%는 background으로 잘못 예측
- background (실제) → 91%는 잘 맞춤, 9%는 lane이라고 오예측함






