# Travel-recommendation-AI(여행 추천 Ai)
---
# 차례
- [프로젝트 개요](https://github.com/khdbsfdk/Travel-recommendation-AI/blob/main/README.md#%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EA%B0%9C%EC%9A%94)
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
#### (3) 챗봇 데이터 생성
- 참고할 데이터를 찾지 못하여 직접 생성했습니다.
- 사용한 코드는 다음과 같습니다.
``` python
people = ['가족들과', '가족과', '친구들과', '친구와', '친구랑', '애인과', '애인이랑', '여자 친구와',
          '남자 친구와', '여자 친구랑', '남자 친구랑', '부모님과', '부모님과 함께', '아이들과',
          '애들과', '애들이랑', '애들 데리고', '어머니와', '아버지와', '혼자서', '나 혼자서', '혼자', '홀로']
place = ['오름', '둘레길', '숲', '공원', '섬', '휴양림', '계곡', '산', '등산길', '해수욕장', '해변', '리조트',
        '온천', '폭포', '박물관', '아쿠아리움', '테마 파크', '전시관', '미술관', '관광 명소', '올레길', '행사',
        '야영장', '산책로', '일몰 명소', '수영장']
# 라벨 지정
def find_thema(word, dict_thema):
    dict_thema_list = ['관광 명소','역사', '자연', '사진', '도보', '예술', '육상', '수상', '공중', '봄', '여름',
                        '가을', '겨울', '사계절', '어린이', '혼자', '친구', '커플', '부모', '가족']
    for i in dict_thema_list:
        if word in dict_thema[i]:
            break
        else:
            continue
    return i

Q_data = []
key = []
# 예시1 -> {사람들과} 갈만한 {장소} 추천해줘
for p in people:
    for i in place:
        key_a = []
        sentence = f"{p} 갈만한 {i} 추천해줘"
        key_1 = find_thema(p, dict_thema)
        key_2 = find_thema(i, dict_thema)
        if key_1 != key_2:
            key_a.append(key_1)
            key_a.append(key_2)
        elif key_1 == key_2:
            key_a.append(key_1)
        Q_data.append(sentence)
        key.append(key_a)
print(Q_data)
print(key)
```
- 이렇게 생성하여 만든 데이터 예시 사진입니다.
<img width="100%" src="https://user-images.githubusercontent.com/84302953/165202738-472c6e1d-0cf9-4fc9-b6d1-b4a84e44ce46.png"/>

#### (4) 챗봇 학습 진행
- 제가 사용한 모델은 transformers의 bert입니다.
``` python
model = SentenceTransformer('sentence-transformers/xlm-r-100langs-bert-base-nli-stsb-mean-tokens')
```
- 저장한 챗봇 데이터 프레임에 임베딩 값을 구한 후 코사인 유사도를 구합니다.
<img width="100%" src="https://user-images.githubusercontent.com/84302953/165212133-f03b723b-d3e9-443d-9a0e-6c6d266dd420.png"/>
- 질문 문장을 넣으면 학습 문장 중 가장 유사한 문장을 찾아 답변합니다.
<img width="100%" src="https://user-images.githubusercontent.com/84302953/165212338-c943ad19-318f-4ed3-bc38-e0bd1c7dbf46.png"/>

## 프로젝트 수행 절차 - 추천 알고리즘
#### (1) 데이터 수집
- 데이터는 한국 관광 데이터랩에서 가져왔으며, 필요한 추가 정보는 visit jeju사이트에서 크롤링했습니다.
- https://colab.research.google.com/drive/1EzFI03uDONkWwgk0zRkL_5I8fnkUSdk8#scrollTo=54fd38cc 
