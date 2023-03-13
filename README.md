# 2022년 제2회 소방안전 AI예측 경진대회

## 공모 일정 (22.10.17 ~ 22.11.30)

## 문제 정의 및 목표
구급 출동 요청 건수가 급증하면서, 사전에 많은 신고가 예상되는 장소를 파악하여 대비하는 것이 중요합니다. 

이를 통해 골든타임을 놓치는 경우를 최소화할 수 있습니다. 

그러나, 단순히 구급 출동 데이터만으로는 장소를 정확하게 예측하기 어려우므로, 

외부 정보를 추가하여 예측 정확도를 높이는 것이 필요합니다.

## 데이터셋
  1. 기본 데이터 : 격자(1000m) 단위 구급출동, 인구, 소방지수 데이터 제공

    - 공간적 범위 : 강원도 원주시

    - 시간적 범위 : 2021년 1월 ~ 2021년 12월

  2. 외부 데이터 : 외부 정보(적설량, 노인인구 밀집 지역, 식당가 등)를 추가하여 격자별로 데이터를 가공

## 공모전 참여 인원 및 역할 
|                이름                           |                  역할                 |
| :-------------------------------:             | :------------------------------------: |
|  [손용원](https://github.com/ywonson)         |      Data Analyst, Data Modeling      |
|  [심재만](https://github.com/shimjaeman)      |     Project Manager, Data Scientist   |
|  [최규광](https://github.com/kyukwnag)        |      Data Analyst, DATA Scientist     |

## Tech Stack
<div align=left> 
 <img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white"> 
 <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white"> 
 <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
 <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
 
## 구동 알고리즘 및 모델링 
  * Modeling Page [ [Modeling](https://github.com/shimjaeman/Fire_Safety_Competition/tree/main/04.%20Modeling) ]

## 최종 결과
  * 우수상 수상 [ https://github.com/shimjaeman/Fire_Safety_Competition/issues/1#issue-1620694810 ]

## 결론 및 한계점
  * 사고가 발생한 건수가 너무 적어서 전체 데이터를 undersampling하는 것이 어려웠습니다.
  
  * 각 사고별로 모델을 만들려고 했는데, 이를 함수화하지 않아서 작업이 어려웠습니다.
  
  * 유동인구가 없거나 사건이 발생하지 않은 지역을 제외하다 보니 해당 지역의 사고 발생 예측이 어려웠습니다.

## 참고논문 및 사이트
  * XGBoost : https://xgboost.readthedocs.io/en/stable/
  
  * RandomForestClassifier : https://www.datacamp.com/tutorial/random-forests-classifier-python
  
  * CatBoost : https://catboost.ai/en/docs/concepts/python-reference_catboostclassifier
  
  * AutoML : https://pycaret.gitbook.io/docs/
