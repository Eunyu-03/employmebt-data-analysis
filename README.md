## 📊 1. 데이터 분석

### 📌 분석 목적

청년층 고용 감소의 사회적 문제를 정량적으로 진단하고, 이를 바탕으로 플랫폼의 필요성과 사회적 가치를 데이터 기반으로 설명하고자 하였다.  
이를 위해 **KOSIS**(국가통계포털)에서 제공하는 고용 데이터를 수집하고, `pandas`, `numpy`, `matplotlib`를 활용하여 분석을 수행하였다.


### 🧪 데이터 수집 및 전처리

- **데이터 출처**: [KOSIS 국가통계포털](https://kosis.kr)
- **분석 대상**: 2025년 5월 ~ 10월 기준, 연령대별 취업자 수 (단위: 천 명)
- **사용 라이브러리**:

  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  ```

### 🧪 전처리 과정

- 연령대별 시계열 데이터를 `DataFrame`으로 구성  
- 날짜 형식 통일 및 인덱스 설정  
- 결측치 및 이상치 확인 후 보간 처리  


### 📈 시각화 결과

<div style="display: flex; justify-content: center; gap: 20px;">
  <img src="https://github.com/user-attachments/assets/b93b5b2b-fe99-4cc6-a47f-18d86a766a6e" width="400" />
  <img src="https://github.com/user-attachments/assets/cfdf8ae2-65cd-4367-b50d-2a6550aea365" width="400" />
</div>

- **왼쪽 그래프**: 청년층(15~29세) 취업자 수 추이  
- **오른쪽 그래프**: 30세 이상 취업자 수 추이

#### 구현 코드
```python
df = pd.read_csv("./datasets/employment_rate.csv")

months = df.columns[2:]

youth = df[(df["성별"] == "계") & (df["연령계층별"] == "15 - 29세")][months].values.flatten()

senior_30_39 = df[(df["성별"] == "계") & (df["연령계층별"] == "30 - 39세")][months].values.flatten()
senior_40_49 = df[(df["성별"] == "계") & (df["연령계층별"] == "40 - 49세")][months].values.flatten()
senior_50_59 = df[(df["성별"] == "계") & (df["연령계층별"] == "50 - 59세")][months].values.flatten()
senior_60_plus = df[(df["성별"] == "계") & (df["연령계층별"] == "60세이상")][months].values.flatten()

# 청년층 고용 통계
plt.figure(figsize=(10, 5))
plt.plot(months, youth, marker='o', color='blue', label='Youth (15–29)')
plt.title('Youth Employment Trend (May–Oct 2025)')
plt.xlabel('Month')
plt.ylabel('Number of Employed')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# 청년층 제외 고용 통계
plt.figure(figsize=(10, 6))
plt.plot(months, senior_30_39, marker='o', label='Age 30–39')
plt.plot(months, senior_40_49, marker='o', label='Age 40–49')
plt.plot(months, senior_50_59, marker='o', label='Age 50–59')
plt.plot(months, senior_60_plus, marker='o', label='Age 60+')
plt.title('Senior Employment Trend (May–Oct 2025)')
plt.xlabel('Month')
plt.ylabel('Number of Employed')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
```


### 🔍 분석 결과 및 해석

청년층(15~29세) 취업자 수는 2025년 5월 **3682천 명**에서 10월 **3521천 명**으로 약 **4.4% 감소**  
→ 특히 **20대 초반**에서 하락폭이 두드러졌으며, 이는 실무 경험 부족 및 직무 이해도 부족과 연관된 것으로 해석됨

30세 이상 취업자 수는 같은 기간 동안 **안정적인 유지**  
→ 일시적 공백(출장, 육아휴직 등)은 존재하지만, 전체 고용 규모에는 큰 변동 없음


### 🧩 인사이트 및 서비스 기획 연계

청년층 고용 감소와 기성 세대의 고용 안정성 사이의 간극을 데이터로 확인

이 간극을 활용하여, 다음과 같은 **실무 중심 고용 모델**을 제안:

> “재직자의 일시적 공백을 청년이 단기 체험으로 메우는 구조”
