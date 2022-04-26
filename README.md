# Travel-recommendation-AI(여행 추천 Ai)
---
# 차례
- 소개
- 프로젝트 개요
- 프로젝트 수행 절차
  - 웹
  - 챗봇
  - 추천 알고리즘
- 참고 자료
---
## 프로젝트 개요
#### (1)프로젝트 선정 및 선정 배경
- 보통 여행지 추천은 키워드로 추천하지만 본 프로젝트는 사용자의 요구를 대화로 받아 절차를 간소화하고 더 쉽게 여행지를 추천합니다.
#### (2)프로젝트 구현 내용
- 추천 알고리즘 -> 기계학습, 알고리즘 처리
- 챗봇 -> 자연어 처리
#### (3)프로젝트 의의
- 지금까지 받은 교육에서는 단순히 데이터 분석 및 모델 개발만 배웠다면 프로젝트를 통해 데이터 수집 및 전처리 능력을 더욱 향상 시킬 수 있습니다.
#### (4)개발 환경
- 코랩 or 주피터 노트북
#### (5)기대 효과
- 사용자가 직접 여행지를 고르지 않아도 여행지를 골라주어 편합니다. 또한, 사용자의 니즈가 잘 반영된다면 여행 만족도 상승 및 색다른 여행을 기대할 수 있습니다.
---
## 프로젝트 수행 절차 - 웹
- 웹은 플라스크로 구현하여 했으나 실패했습니다.
- 따라서 tkinter로 대체했습니다.

## 프로젝트 수행 절차 - 챗봇
#### (1) 챗봇을 사용한 이유
- 버튼이 아닌 대화를 통해 사용자에게 정보를 받아 여행지를 추천하고자 했습니다.
- 사용자가 직접 여행지를 고르지 않아도 **맞춤형**으로 여행지를 골라주어 **색다른 여행**이 가능합니다.
#### (2) 챗봇의 종류
- 저는 챗봇을 크게 2가지로 나누었습니다.
  1. 최대한 적은 대화로 사용자가 원하는 것을 이해하고 **해결**해주려는 목적을 가진 **문제 해결용 대화 시스템**
  2. 사용자가 어떠한 주제로 말을 걸면, 시스템에 맞는 답변을 하며 **대화**를 이어나가는 **자유 주제 대화 시스템**
- 본 프로젝트는 여행지 추천에 중점을 두었고, 간단한 인사만 가능한 챗봇을 목적으로 합니다.
- 따라서 문제 해결용 대화 위주의 챗봇을 제작했습니다.
#### (3)
