# Multi-Object Tracking 평가 지표 (Evaluation Metrics)

## 1. MOTA (Multi-Object Tracking Accuracy)

**의미**: 전체 추적 정확도를 종합적으로 평가하는 지표 (FN, FP, ID switch 포함)  
**수식**:

$$
\text{MOTA} = 1 - \frac{\sum_t (FN_t + FP_t + ID\_SW_t)}{\sum_t GT_t}
$$

| 항목     | 의미                                  |
|----------|---------------------------------------|
| FN       | 놓친 객체 (False Negative)           |
| FP       | 잘못 검출된 객체 (False Positive)     |
| ID\_SW   | 객체 ID가 잘못 바뀐 횟수 (ID Switch) |
| GT       | Ground Truth 객체 수                 |

➡️ **값이 높을수록 좋음** (↑)

---

## 2. MOTP (Multi-Object Tracking Precision)

**의미**: 추적된 객체의 위치 정밀도 (Bounding Box 오차 평균)  
**수식**:

$$
\text{MOTP} = \frac{\sum_{i,t} d_{i,t}}{\sum_t \text{매칭된 객체 수}}
$$

- \( d_{i,t} \): i번 객체의 프레임 t에서의 위치 오차 (예: IoU 거리)

➡️ **값이 낮을수록 좋음** (↓)

---

## 3. IDF1 (ID F1 Score)

**의미**: 객체 ID의 유지 성능 (정확성과 일관성의 조화 평균)  
**수식**:

$$
\text{IDF1} = \frac{2 \times \text{ID Precision} \times \text{ID Recall}}{\text{ID Precision} + \text{ID Recall}}
$$

- ID Precision: 올바르게 추적된 ID / 전체 예측 ID 수  
- ID Recall: 올바르게 추적된 ID / 전체 GT ID 수

➡️ **값이 높을수록 좋음** (↑)

---

## 4. HOTA (Higher Order Tracking Accuracy)

**의미**: Detection 정확도와 Association 정확도를 조화롭게 평가하는 최근 대표 지표  
**수식** (개요):

$$
\text{HOTA} = \sqrt{\text{DetA} \times \text{AssA}}
$$

- DetA: Detection Accuracy (검출 정확도)  
- AssA: Association Accuracy (ID 일관성)

➡️ **값이 높을수록 좋음** (↑)

---

## 5. ID Switch (ID\_SW)

**의미**: 동일 객체를 추적하다가 ID가 바뀐 횟수 (오연결)  
➡️ **값이 낮을수록 좋음** (↓)

---

## 6. Mostly Tracked (MT) / Mostly Lost (ML)

| 항목 | 의미 |
|------|------|
| MT   | 전체 프레임의 ≥ 80% 동안 올바르게 추적된 객체 비율 → **높을수록 좋음** (↑) |
| ML   | 전체 프레임의 ≤ 20%만 추적된 객체 비율 → **낮을수록 좋음** (↓) |

---

## 📋 요약 비교표

| 지표명   | 의미                               | 목표 |
|----------|------------------------------------|------|
| MOTA     | 전체 추적 오류 종합 정확도         | ↑    |
| MOTP     | 추적 위치 정밀도                   | ↓    |
| IDF1     | ID 유지 정확도 (정확성+일관성)     | ↑    |
| HOTA     | 검출 + 연관 조화 평균              | ↑    |
| ID\_SW   | ID가 바뀐 횟수                     | ↓    |
| MT       | 대부분 성공적으로 추적된 객체 비율 | ↑    |
| ML       | 거의 추적되지 못한 객체 비율       | ↓    |
