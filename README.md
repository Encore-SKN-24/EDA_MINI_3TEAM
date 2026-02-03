# 🍷 [팀명 입력]: 술과 수명, 그 상관관계의 진실을 찾아서
> **"술을 많이 마시면 정말 수명이 짧아질까?"** 라는 호기심에서 시작된 WHO & World Bank 글로벌 보건 데이터 EDA 프로젝트

---

## 1. 👥 팀 소개
| 성함 | GitHub / Blog |
| :---: | :---: |
| **[이름1]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/) |
| **[이름2]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/) |
| **[이름3]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/) |
| **[이름4]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/) |
| **[이름5]** | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white)](https://github.com/) |

---

## 2. 📋 프로젝트 개요

### 💬 Project Story
저희 팀은 "술을 좋아하는 사람들이 건강하게 오래 살 방법은 없을까?"라는 가벼운 수다에서 분석을 시작했습니다. 

단순히 **'술 소비량'**과 **'기대수명'**은 정비례하거나 반비례할 것이라 예상했지만, 실제 데이터를 맛보기로 EDA 해보니 결과는 예상보다 훨씬 복잡했습니다. 술 외에도 경제적 풍요로움, 보건 인프라, 교육 수준 등 수많은 변수가 얽혀 있었죠. 

그래서 저희는 **"기대수명을 결정짓는 진짜 'Key Factor'는 무엇인가?"**를 밝혀내기 위해 제대로 된 EDA를 진행하게 되었습니다.

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
