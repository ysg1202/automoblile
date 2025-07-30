# 🧠 NVIDIA PeopleNet ONNX 추론 노트북 정리

## 📌 개요
이 문서는 `NVIDIA PeopleNet` 모델을 ONNX 형식으로 추론하기 위한 Python 코드 흐름과 사용된 핵심 라이브러리인 `onnxruntime`에 대해 정리한 것입니다.

---

## 🧩 1. ONNX란?

- **ONNX(Open Neural Network Exchange)**는 서로 다른 프레임워크 간에 AI 모델을 호환 가능하게 해주는 **중립적인 모델 저장 형식**입니다.
- 예: PyTorch에서 학습한 모델을 ONNX로 export하여 TensorRT, OpenVINO, ONNX Runtime 등에서 사용할 수 있습니다.

---

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

