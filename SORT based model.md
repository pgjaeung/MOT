# Object Tracking 일지

## 1. OC-SORT  
**설명:**  
SORT 모델의 한계인 비선형 운동에 대해 더 robust하게 개선한 모델.  
OCR, OCM, OOS 등의 method를 통해 성능 보완.

**Limitation:**  
- 낮은 FPS의 영상이나 object의 움직임이 매우 빠른 경우, IoU와 momentum만으로는 매칭에 부족함  
- Kalman filter를 개선했으나, 여전히 **선형 움직임을 가정한 모델**

---

## 2. Deep OC-SORT  
**설명:**  
OC-SORT에 appearance 정보를 통합하여 단순 motion-based matching의 한계를 극복.  
외형 임베딩을 활용해 ID switch 문제를 줄이고, occlusion 상황에서도 추적 성능 향상.

**Limitation:**  
- 외형 특징 의존성: 조명 변화나 객체 자세 변화에 따라 성능 저하 발생  
- 계산 복잡도 증가: appearance 통합으로 연산량 증가, 실시간 처리 부담

---

## 3. PD-SORT (Pseudo-Depth SORT)  
**설명:**  
2D 비디오에서 추정된 pseudo-depth 정보를 활용해 객체 간 거리 정보 보강.  
DVIoU, QPDM을 도입하여 IoU 기반 매칭의 한계를 보완.

**Limitation:**  
- 깊이 정보의 한계: Pseudo-depth는 정밀한 3D depth가 아니므로 복잡한 장면에서 신뢰도 저하  
- 군중 환경에서의 성능 저하: 유사한 depth를 가진 객체들이 밀집한 경우 구분력이 떨어짐

---

## 4. AM-SORT (Adaptable Motion SORT)  
**설명:**  
Kalman filter 대신 Transformer 기반 motion 예측기를 사용하여 비선형 운동에 대한 예측 정확도를 향상.  
이전 시점(t)의 정보를 Transformer에 입력해 움직임을 예측.

**Limitation:**  
- Appearance 정보 미활용: Motion 정보만 사용하면 유사 궤적 간 ID switch 문제 발생  
- 추론 속도 저하: Transformer 구조 특성상 실시간 적용에는 한계 존재

---

## 5. MambaMOT  
**설명:**  
State-space model을 기반으로 Kalman filter의 선형 가정을 극복.  
복잡한 비선형 운동과 occlusion이 빈번한 환경에서도 높은 추적 정확도를 유지.

**Limitation:**  
- 복잡한 구조: 구현 및 튜닝 난이도가 높음  
- 학습 데이터 의존성: 성능 확보를 위해 충분하고 다양한 학습 데이터 필요

