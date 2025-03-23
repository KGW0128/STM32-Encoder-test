# 엔코더 사용 및 설정

## 엔코더 설명

### 1. **A 신호 (Phase A)**
- **기본 역할**: A 신호는 엔코더의 **기본 출력 신호**로, 회전 방향과 위치를 추적합니다. A 신호는 **펄스 형태**로 출력되며, 회전하는 동안 **주기적으로 High와 Low 값이 교차**합니다.
- **용도**: A 신호의 **상승 또는 하강 엣지**를 기반으로 카운팅하여 **각도 변화**를 추적합니다.

### 2. **B 신호 (Phase B)**
- **기본 역할**: B 신호는 **A 신호와 90도 위상 차이를 두고 출력**됩니다. B 신호는 A 신호보다 **90도 지연된** 신호로, 회전 방향을 **판단**합니다.
- **용도**: A와 B의 **위상 차이**를 비교해 회전 방향을 파악할 수 있습니다.

### 3. **Z 신호 (Index Pulse)**
- **기본 역할**: Z 신호는 **한 바퀴 회전**에 대해 정확히 **1번만 발생**하는 신호입니다. 이를 통해 **0도 기준**을 설정하거나 **위치 초기화**를 할 수 있습니다.
- **용도**: Z 신호는 **절대적인 참조점**으로 사용되며, 매 회전마다 **정확한 초기화**를 할 수 있습니다.

### **Z 신호 사용법**
- **Z 신호**는 **GPIO_EXTI** 핀에 연결하여 사용하면, 펄스가 계속 감소하지 않고 고정됩니다. **기준점 설정**을 통해 펄스 값이 변하지 않도록 할 수 있습니다.

---

## STM32 연결

### 핀 사용
- 엔코더의 **A**, **B**, **Z** 신호를 STM32의 핀에 연결하여 사용합니다.

### TIM3 엔코더 세팅
- 엔코더는 **TIM3** 타이머를 사용하여 설정합니다. 다른 타이머를 사용해도 동일한 방식으로 설정 가능합니다.

### 엔코더 회전수와 펄스 설정
- 엔코더가 **5000 PPR**인 경우, **4배 증폭 설정 (x4)**을 사용하여 **20,000 펄스**로 설정합니다. 이렇게 하면, **해상도를 높여** 더 정확한 각도 추적이 가능합니다.

### 왜 5000에서 20000으로 설정하는가?
- **4배 증폭**을 통해 A와 B 채널의 신호 변화를 모두 카운팅할 수 있어, 엔코더의 해상도를 **4배 높일 수 있습니다**. 이를 통해 **정밀한 위치 제어**가 가능해집니다.

---

## 주의사항
- **엔코더는 항상 고정된 상태에서 사용**해야 합니다. 엔코더가 **살짝 움직이면** 값이 변동될 수 있습니다.
- **엔코더는 현재 시작지점 기준으로 작동**하며, **빌드 시점의 시작 위치**를 기준으로 **0도**가 설정됩니다. 따라서, 실행할 때마다 **0도 위치가 달라질 수 있습니다**.

---

### 추가 자료
- **[Z 신호 사용법 영상](https://www.youtube.com/watch?v=6oXmkOyYzyg)**
- **[E40 엔코더 PDF](attachment:e40.pdf)**
