# 서울과학기술대학교 AI COSS X A.ing X Lailac Hackathon

Kumar 2-Layer CNN (전처리 포함)

## 1. 개요

본 프로젝트는 Kumar et al.(2024)의 2계층 CNN 구조를 기반으로 한 다중 클래스 이미지 분류 모델입니다.

전처리와 정규화를 적용하여 **일반화 성능**을 향상시켰습니다.

**최종 성능 (내부 검증 기준):**

- 정확도 (Accuracy): **98.76%**
- F1 점수 (Macro): **0.9876**

## 2. 환경 설정

### 필수 라이브러리 설치

```bash
pip install -r requirements.txt
```

## 3. 모델 평가 실행 방법

학습된 가중치(`best_model.pth`)를 자동으로 불러와

`./test` 폴더 내의 이미지 데이터를 평가합니다.

inference.ipynb
→ 저장된 가중치(best_model.pth)를 불러와 테스트 세트를 평가
→ 정확도, F1 점수, 혼동행렬(Confusion Matrix) 자동 출력

requirements.txt
→ 라이브러리 설치를 위한 패키지 목록
---

## 4. 디렉터리 구조

```
./
├── best_model.pth     # 학습된 모델 가중치
├── inference.ipynb    # 평가용 스크립트 (심사용)
├── model.ipynb        # 학습 재현용 스크립트 (선택사항)
├── requirements.txt   # 라이브러리 목록
└── README.md          # 설명서

```

---

## 5. 모델 정보

| 항목 | 설명 |
| --- | --- |
| **모델 구조** | Custom 2-Layer CNN (Kumar et al., 2024) |
| **입력 크기** | 128×128 RGB |
| **정규화(Normalize)** | mean = [0.4002, 0.4313, 0.4276], std = [0.2648, 0.1987, 0.1455] |
| **데이터 증강** | Random Flip, Rotation, Perspective, ColorJitter |
| **최적화 알고리즘** | Adamax (lr=0.001) |
| **스케줄러** | ReduceLROnPlateau (factor=0.5, patience=5) |
| **정규화 기법** | Dropout(0.3), BatchNorm, Early Stopping |
| **안정화 기법** | EMA(Exponential Moving Average)로 검증 곡선 스무딩 |

---

## 6. 실행 결과 예시

inference.ipynb 실행 시 다음과 같은 결과가 출력됩니다.

```
================= 📊 Test Performance =================
✅ Test Accuracy: 98.76%
✅ Test F1 Score (macro): 0.9876
========================================================

```

혼동행렬(Confusion Matrix) 또한 실행 시 시각적으로 표시됩니다.

---

## 7. 참고 사항

모든 경로는 상대경로(./best_model.pth, ./test/) 기준으로 작성되었습니다.

만약 심사 환경에서 경로 인식 오류가 발생할 경우,
심사위원님 환경의 실제 경로에 맞게 수정하여 실행해 주시기 바랍니다.

예를 들어:

test_dir = "C:/Users/.../test"
model_path = "C:/Users/.../best_model.pth"

**⚠️ 평가 데이터 경로 안내**

interence.ipynb 내 test/ 폴더는 임의의 예시 데이터로,
모델의 동작 검증용 샘플입니다.

실제 평가 시에는, 심사위원 측 평가용 테스트셋 경로를
./test 대신 해당 환경의 경로로 변경하여 실행하시면 됩니다.

# 예시)
# 기존 코드
test_dir = "./test"

# 평가용 데이터셋 경로로 수정
test_dir = "/path/to/evaluation_dataset"


**실행 안내**
model.ipynb 파일은 학습 재현용입니다.

평가를 위해서는 inference.ipynb만 실행하시면 됩니다.

Jupyter Notebook 환경에서 실행 시,
모든 결과(그래프, 성능 지표, 시각화)가 즉시 출력됩니다.
