# 🎹 [그럴 수 ~ 명있지]: 술과 기대수명의 착시에서 출발해, 오래 사는 진짜 이유를 찾다.
> **"술을 많이 마시면 정말 수명이 짧아질까?"** 라는 호기심에서 시작된 WHO 데이터 EDA 프로젝트

---

## 1. 👥 팀 소개
| 성함 | GitHub |
| :---: | :---: |
| **[권민제]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/min3802) |
| **[문성준]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/dal-sj) |
| **[전윤우]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/Yunu-Jeon) |
| **[정준하]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/junhaj27-jpg) |
| **[최하진]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/hun668486) |

---

## 2. 📋 프로젝트 개요

### 💬 Project Story
“술은 건강에 좋지 않다고 하는데, 술을 많이 마시는 나라의 사람들은 실제로 어떨까?”라는  
가벼운 호기심에서 분석을 시작했습니다.

처음에는 **알코올 소비량**과 **기대수명**이 어느 한쪽으로 뚜렷한 관계를 보일 것이라 예상했지만,  
GDP가 높은 국가일수록 알코올 소비량이 많으면서도 기대수명이 높은 경우가 존재했고,
변수 간 관계는 일관되게 강한 상관관계를 보이지는 않았습니다.

이 과정에서 기대수명은 단순히 술 소비나 경제 수준만으로 설명되기 어렵고,  
**보건 환경, 교육 수준, 질병 관리, 예방접종 등 다양한 요인이 함께 얽혀 있는 지표**임을 확인했습니다.  
따라서 본 프로젝트는 WHO 기대수명 데이터를 활용해  
**사람들이 더 오래 사는 데 영향을 주는 핵심 요인(Key Factors)이 무엇인지**를 탐색하는 것을 목표로 합니다.


### 📚 데이터 출처
* [WHO Global Health Observatory (GHO)](https://www.who.int/data/gho)
* [World Bank Open Data](https://data.worldbank.org/)

---

## 3. 🛠 기술 스택
| 분류 | Stack |
| :--- | :--- |
| **Language** | ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white) |
| **Visualization** | ![Matplotlib](https://img.shields.io/badge/Matplotlib-ffffff?style=for-the-badge&logo=Matplotlib&logoColor=black) |
| **Tool** | ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=Jupyter&logoColor=white) ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=Git&logoColor=white) |

---

## 4. ⚙️ 데이터 전처리 (Preprocessing)
데이터의 무결성을 위해 `isna().sum()` 탐색 후 다음과 같은 **단계별 결측치 처리 로직**을 수립했습니다.

1. **시간적 보간**: 한 국가의 데이터 중 세로(연도) 방향으로 비어있는 경우, 해당 컬럼의 **전후년 평균값**으로 대치합니다.
2. **공간적 보간**: 전후 데이터가 없는 경우, 해당 국가가 속한 **지역(Region)의 평균값**을 활용하여 지역적 특성을 반영했습니다.
3. **데이터 정화**: 위 과정을 거친 후에도 한 국가 내에서 **컬럼이 4개 이상 비어있는 경우**, 데이터 오염을 방지하기 위해 해당 국가의 레코드를 분석 대상에서 **제외**했습니다.

```mermaid
graph LR
    %% 방향을 LR(Left to Right)로 변경하여 가로 공간 확보
    
    %% 노드 정의
    Start([Raw Data])
    Step1{Step 1. 데이터 정화}
    Drop[[DROP: 분석 제외]]
    Step2[Step 2. 시간적 보간]
    Step3[Step 3. 공간적 보간]
    End[(Final Dataset)]

    %% 연결 및 라벨 (긴 라벨에 <br/> 적용)
    Start --> Step1
    
    subgraph P1 [Phase 1: Quality Control]
        %% 텍스트가 길어 겹치는 부분 줄바꿈
        Step1 -- "결측치 >= 4개<br/>(오염 데이터)" --> Drop
    end

    subgraph P2 [Phase 2: Data Imputation]
        Step1 -- "정상 (Pass)" --> Step2
        %% 텍스트 줄바꿈
        Step2 -- "전후 연도<br/>평균값 활용" --> Step3
    end

    %% 텍스트 줄바꿈
    Step3 -- "소속 Region<br/>평균값 활용" --> End

    %% 스타일링 (이전과 동일)
    style Start fill:#f5f5f5,stroke:#9e9e9e,stroke-width:2px
    style Step1 fill:#fff9c4,stroke:#fbc02d,stroke-width:2px
    style Drop fill:#ffebee,stroke:#ef5350,stroke-width:2px,color:#c62828
    style Step2 fill:#e3f2fd,stroke:#2196f3,stroke-width:2px
    style Step3 fill:#e3f2fd,stroke:#2196f3,stroke-width:2px
    style End fill:#e8f5e9,stroke:#4caf50,stroke-width:3px
    
    style P1 fill:#fafafa,stroke:#eeeeee,stroke-dasharray: 5 5
    style P2 fill:#fafafa,stroke:#eeeeee,stroke-dasharray: 5 5
```
---

## 5. 📊 수행 결과

### 🧪 1. 상관관계 분석 (Heatmap)

* **핵심 인사이트**: 히트맵 분석 결과, 예상과 달리 **알코올 소비량은 기대수명과 유의미하게 높은 상관관계를 보이지 않았습니다.** 이는 술 소비량 자체가 수명을 결정짓는 단일 요인이 아님을 입증합니다.

### 🧬 2. PCA(주성분 분석) 및 카테고리별 상세 분석

* **PCA 진행**: 수많은 변수를 경제, 보건, 사회적 요인 등 카테고리별로 묶어 PCA를 수행했습니다.
* **상세 분석 결과**:
  - 알코올보다는 **[GDP/Schooling 등]** 카테고리가 주성분 형성에서 압도적인 가중치를 보였습니다.
  - 해당 카테고리와 기대수명의 관계를 시각화하여 가장 영향력 있는 요인이 **[무엇]**인지 최종적으로 규명했습니다.

---

## 6. 💬 한 줄 회고
* **[이름1]**: "당연한 상식이 데이터 앞에서는 가설일 뿐이라는 점을 배웠습니다."
* **[이름2]**: "결측치 처리 로직을 세우며 데이터 정제의 정교함을 익혔습니다."
* **[이름3]**: "PCA를 통해 복잡한 다차원 데이터를 핵심 중심으로 요약하는 법을 깨달았습니다."
* **[이름4]**: "시각화 라이브러리를 활용해 설득력 있는 리포트를 작성하는 경험을 쌓았습니다."
* **[이름5]**: "팀원들과 함께 흥미로운 주제를 데이터로 증명해가는 과정이 즐거웠습니다."
