# 대구 교통사고 피해 예측 AI 경진대회 (Dacon)  
## 프로젝트 개요
사고 발생 시간, 공간 등의 정보를 활용하여 사고위험도(ECLO)를 예측하는 AI 알고리즘 개발  

※ ECLO(Equivalent Casualty Loss Only) : 인명피해 심각도  
ECLO = 사망자수 * 10 + 중상자수 * 5 + 경상자수 * 3 + 부상자수 * 1 본 대회에서는 사고의 위험도를 인명피해 심각도로 측정  

사용 metric은 RMSLE로 log 스케일 지표다.    
절대적 값의 차이를 확인하기 위해서 MAE랑 RMSE도 함께 사용해서 비교. 

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
1. 대구 교통사고 데이터 (내부 데이터) 확인 및 데이터 전처리    
2. 외부 데이터 (CCTV, 보호등, 어린이보호구역, 주차장, 대구 외 지역 교통사고 데이터) 확인 및 데이터 전처리  
3. 내부 데이터에 XGB, LGBM, CatB, MLP 등 여러 모델 적용 후 비교. Optuna로 트리 모델들 최적화 수행.  
4. 데이터를 분할하여 예측  
5. ELCO의 개별적 요소들을 각각의 모델들로 예측해서 통합하여 예측  
6. 전국 데이터 활용  
7. 클러스터링 사용 - K-means, DBSCAN, HAC 등을 통해서 나눈 다음 각각을 예측    

## 프로젝트 세부 과정  
### 1. 대구 교통사고 데이터 (내부 데이터) 확인 및 데이터 전처리  
+ 연, 월, 일, 시, 시, 군, 구, 읍면동 추출  
+ 노면상태, 시, 군, 구, 읍면동의 dummy variable화   

### 2. 외부 데이터 (CCTV, 보호등, 어린이보호구역, 주차장, 대구 외 지역 교통사고 데이터) 확인 및 데이터 전처리  

+ 주차장 데이터 전처리 담당: 구별 주차장의 수, 주차 구획수로 데이터 정제. 주차장 유형, 운영요일은 제외.
+ 대구를 제외한 전국 데이터를 1번과 같이 전처리 후 사용
    + 시군구 데이터를 넣어서 이질적인 데이터로 처리하는 방법
    + 시군구 데이터를 모두 제거하여 동질적인 하나의 데이터로 처리하는 방법

### 3. 모델 선정  

Random Forest, XGBoost (이하 XGB), Light GBM (이하 LGBM), CatBoost (이하 CatB), MLP (Multi-Layer Perceptron)




12/5
Random Forest, 대구데이터로만(Public Score: 0.4399026489)

XGBoost, 대구데이터로만 (OOF Val 0.4488), cctv데이터추가함(Public Score: 0.428448757), 전국데이터(63만) location x(Public Score: 0.4325240971), 전국데이터(63만) location o, 

LGBM, 대구데이터로만, cctv데이터추가함,

ECLO : 각 추론 모델 (사망자, 중상자, 경상자, 부상자) 4개 모델 xgboost로 생성. (Public Score: )

12/6
63만개의 전국 데이터로 XGB. 이때 시군구를 제외하여 같은 데이터로 취급.

K-means, HAC, DBSCAN, HDBSCAN 수행.

기존 RMSLE가 log 스케일이라 변화가 작기 때문에 결과값의 절대적 크기를 잘 보존하는 Absolute Error를 추가적으로 비교. MAE를 또 다른 metric으로 추가한다.

7-means clustering이 데이터를 잘 분할한다고 생각하여 클러스터별로 예측 모델을 만들어서 나중에 aggregate하는 모델 생각. 하지만 아래와 같이 모델 성능이 좋게 나오지 않아서 다른 방법을 모색 중

전국 데이터 MLP 모델 → Best Val RMSLE: 0.4392, Train RMSLE: 0.1098 

12/12 정리
- 대구 교통 사고 데이터. train에만 존재하고 test에 없는 데이터(컬럼들)가 존재.
- 최종 타겟 값은 ECLO인데, 사망자, 중상자, 경상자, 부상자의 Weighted Sum.
- train과 test 모두 가지는 데이터만 활용하여 RF, XGB, LGBM, CatB를 활용하여 성능 측정
- Tree Based 모델은 모두 Optuna로 하이퍼파라미터 튜닝. 제일 중요한 하이퍼파라미터를 고정하고 나머지 하아퍼파라미터들을 튜닝하는 방식 자동화.
- Poisson Regression과 numpy Clip을 비교했으나 Poisson이 더 잘 작동.
- MLP를 사용하여 성능 측정. Layers와 Hidden Dim을 바꿔가며 진행.
- 대구 뿐만 아니라 다른 지역 데이터까지 사용한 전국 데이터를 활용하여 MLP, XGB 모델 적용
- 지역이 아니라 사고별로, 유형별로 차이가 있으리라 생각해서 클러스터링 수행
    - K-Means, DBSCAN, HAC, DBSCAN 수행 후 t-SNE로 시각화
    - K-Means과 t-SNE

- 사망자를 제외한 중상자, 경상자, 부상자는 큰 값들을 가지는 모델들을 별도로 학습. 데이터가 많으면 XGB, 적으면 RF로 예측.
    - 사망자수- 하나의 모델 XGB
    - 중상자수 - 0과 1만을 이용한 XGB, 2이상(약 N=750)인 모델 RF.
    - 경상자수 - 0과 4만을 이용한 XGB, 5이상(약 N=400)인 모델 RF.
    - 부상자수 - 0과 1만을 이용한 XGB, 2이상(약 N=400)인 모델 RF.
- 보통 RMSLE가 0.4~0.5의 값이 나오는것과 다르게 세부적인 모델들은 0.05~0.4의 좋은 수치를 보여줌.
- Test 데이터의 경우 사망자수, 중상자수, 경상자수, 부상자수 데이터가 없어서 그룹별로 예측이 불가능.
- 각 모델들을 Weighted Sum해서 Test 데이터의 ECLO를 예측.

사망자 모델은 1, 중상자 모델은 0.8와 0.2, 경상자는 0.9와 0.1, 부상자도 0.9와 0.1

ex) 중상자 예측치 = 중상자XGB예측*0.8 + 중상자Rf예측*0.2

최종 예측 결과는 Public Score가 0.6803로 개별 모델들이 오버피팅이 있었던것으로 추정.  

- 12/08 금요일에 CCTV, 어린이보호구역, 보호등, 주차장 등의 외부 데이터를 모두 합침.
- 4개의 외부 데이터를 모두 사용하여 XGB, LGBM, MLP, 중상자, 경상자, 부상자를 나눠서 예측한 모델 학습.
- 최종적으로는 동별 CCTV의 연도별 총합만을 더한 XGB (하이퍼파라미터 튜닝 완료)한 모델이 가장 좋은 성능.

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
Categorical Data를 integer들로 처리하지 않고 모두 One-Hot으로 처리하는 모델들이 많았다.
Categorical Data를 Target Encoder로 처리하는 경우도 많았다.
AutoML, 트리기반 모델들이 주로 많이 쓰인다.


