# 🧠 NVIDIA PeopleNet

## 🧠 PeopleNet 모델이란?

## 📌 개요
**PeopleNet**은 NVIDIA에서 만든 **사람 관련 객체 탐지 모델**입니다.

> 즉, **사람**, **가방**, **얼굴** 같은 걸 자동으로 찾아내는 모델이에요.

---

## 👀 PeopleNet이 찾을 수 있는 것들

| 클래스 | 설명 |
|--------|------|
| `person` | 사람 |
| `bag` | 가방 (백팩, 핸드백 등) |
| `face` | 얼굴 (정면 인식 가능) |

---

## 📦 PeopleNet은 어떤 용도로 쓰이나요?

- CCTV 사람 감지
- 공공장소 보안 감시
- 로봇이나 자율주행의 사람 인식
- 혼잡도 분석 (사람이 얼마나 많은지)

---

## 🏎️ 특징 요약

| 항목 | 설명 |
|------|------|
| 만든 곳 | NVIDIA |
| 구조 | ResNet 기반 (ex. ResNet34) |
| 사용 환경 | GPU/CPU, Jetson, Edge 디바이스 등 |
| 형식 | `.etlt`, `.onnx`, `.engine` 등 다양한 추론용 파일 제공 |
| 사전 학습 | 이미 사람/가방/얼굴 데이터셋으로 학습 완료됨 (우리가 다시 학습할 필요 없음) |

---

## 🧪 PeopleNet ONNX 모델 예

이 노트북에서는 아래 모델을 사용 중입니다:

```
resnet34_peoplenet_int8.onnx
```

- `resnet34`: ResNet-34 백본
- `int8`: INT8 정수형으로 양자화되어 빠른 추론 가능
- `.onnx`: ONNX 형식으로 어디서든 실행 가능

---

## 🔧 PeopleNet을 어떻게 써요?

1. PeopleNet ONNX 모델 파일을 다운로드
2. `onnxruntime`으로 불러오기
3. 이미지/영상에 사람·가방·얼굴 탐지
4. 사각형 박스로 시각화하거나 결과 저장


## 🧩 1. ONNX란?

- **ONNX(Open Neural Network Exchange)**는 서로 다른 프레임워크 간에 AI 모델을 호환 가능하게 해주는 **중립적인 모델 저장 형식**입니다.
- 예: PyTorch에서 학습한 모델을 ONNX로 export하여 TensorRT, OpenVINO, ONNX Runtime 등에서 사용할 수 있습니다.
- 작은 디바이스(라즈베리파이, Jetson 등)에서도 사용 가능
- 속도 최적화:	ONNX Runtime, TensorRT 등에서 매우 빠르게 실행 가능
- 범용성:	PyTorch, TensorFlow, Keras 등 어떤 툴에서든 변환 가능
---

## 🛠️ ONNX 실제 동작 과정
- 모델 학습: PyTorch나 TensorFlow로 모델을 학습시킴
- ONNX로 변환: model.onnx 파일로 저장
- 추론 도구에서 사용: ONNX Runtime이나 TensorRT, OpenVINO 등에서 실행

### ONNX 파일
- ONNX 모델은 .onnx 확장자를 가지며 내부에는 입력/출력 텐서 정보, 네트워크 구조, 각 레이어의 파라미터가 포함 

## ⚙️ 2. ONNX Runtime이란?

- Microsoft에서 개발한 **ONNX 모델 실행 엔진**입니다.
- 장점:
  - CPU 및 GPU 지원
  - 빠른 추론 성능
  - 경량화
- 설치:
  ```bash
  pip install onnxruntime
  ```

---

## 🧬 3. PeopleNet 모델 정보

- 사용 모델: `resnet34_peoplenet_int8.onnx`
- 클래스:
  ```python
  ['person', 'bag', 'face']
  ```

---

## 🛠️ 4. 코드 흐름 요약

### 1. 필요한 라이브러리 설치
```python
!pip install onnxruntime yt-dlp opencv-python numpy
```

### 2. ONNX 모델 클래스 정의
```python
class DebugNVIDIAPeopleNet:
    def __init__(self):
        self.model_path = "/workspace/peoplenet_vpruned_quantized_decrypted_v2.3.4/resnet34_peoplenet_int8.onnx"
        self.classes = ['person', 'bag', 'face']
        self.colors = [(0, 255, 0), (255, 0, 0), (0, 0, 255)]
        self.setup_model()
```

### 3. 모델 로드 및 ONNX Runtime 세션 설정
```python
self.session = ort.InferenceSession(self.model_path, providers=['CPUExecutionProvider'])
self.input_name = self.session.get_inputs()[0].name
self.output_names = [output.name for output in self.session.get_outputs()]
```

### 4. 모델 입력/출력 형태 확인
```python
input_info = self.session.get_inputs()[0]
print(f"입력: {input_info.name}, 형태: {input_info.shape}")
```

### 5. 모델 추론 실행 (예: `self.test_model()` 내부)
```python
outputs = self.session.run(self.output_names, {self.input_name: input_blob})
```

---

## 🧾 5. 향후 확장

- 영상 또는 이미지 입력 처리: `cv2.VideoCapture`, `cv2.resize`, `cv2.imshow`
- 후처리: confidence threshold, NMS
- 시각화: bounding box + class name overlay

