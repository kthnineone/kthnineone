# 대구 교통사고 피해 예측 AI 경진대회
## 프로젝트 개요
사고 발생 시간, 공간 등의 정보를 활용하여 사고위험도(ECLO)를 예측하는 AI 알고리즘 개발  

※ ECLO(Equivalent Casualty Loss Only) : 인명피해 심각도  
ECLO = 사망자수 * 10 + 중상자수 * 5 + 경상자수 * 3 + 부상자수 * 1 본 대회에서는 사고의 위험도를 인명피해 심각도로 측정  

팀 프로젝트: 4명   
역할: EDA, 피쳐 엔지니어링, 모델링  
진행기간: 2023.12.03 ~ 2023.12.11  
소속 : 패스트캠퍼스&업스테이지 AI Lab 1기 (AI Lab 2기)  


## 기술 스택
+ Scikit-Learn
+ Numpy
+ Pandas
+ XGBoost
+ CatBoost
+ LightGBM
+ optuna
+ matplotlib
+ PyTorch  


## 프로젝트 진행 단계  
데이터 확인  
외부 자료 확인  
XGB, LGBM, CatB, MLP 등 여러 모델 비교  
데이터를 분할하여 예측  
ELCO의 개별적 요소들을 각각의 모델들로 예측해서 통합하여 예측  
전국 데이터 활용  
클러스터링 사용 - K-means, DBSCAN, HAC 등을 통해서 나눈 다음 각각을 예측    

## 프로젝트 세부 과정  
추후 작성 예정  


## 프로젝트 결과  
Public Score: 0.42844  
Private Score: 0.42857  

총 914명 참여  
Public 등수: 269등  
Private 등수: 215등  


1위의 스코어들  
Public Score: 0.42529  
Private Score: 0.4253  


## 프로젝트 회고  
파생 변수 생성이 중요하다  
1, 2위 팀을 보니 공공 데이터의 추가가 중요하다.  
종합하자면 데이터의 질과 양이 매우 중요하다  



