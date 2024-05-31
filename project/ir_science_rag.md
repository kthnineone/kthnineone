# Scientific Knowledge Question Answering  
## 프로젝트 개요
패스트캠퍼스&업스테이지 AI Lab 1기 자체 대회  

과학 지식 질의 응답 시스템 구축  

LLM은 최근 좋은 성능을 보이지만 Hallucination과 Knolwedge Cut-off 현상이 있다.  
위 단점을 극복하기 위해서 RAG (Retrieval Augmented Generation)를 도입한다.  
RAG는 질문에 적합한 레퍼런스 추출을 위해 검색엔진을 활용하고 답변 생성을 위해 LLM(Large Language Model)을 활용한다.  

Puiblic과 Private은 각각 Random하게 5:5로 나뉜다.

평가 지표는 mAP (mean Average Precision)  
mAP는 질의 N개에 대한 Average Precision의 평균 값을 구하고, Average Precision은 Precision-recall curve에서 아래쪽 면적을 의미한다.  


팀 프로젝트: 5명   
역할: EDA, 피쳐 엔지니어링, 모델링  
진행기간: 2024.04.08 ~ 2024.05.02  
소속 : 패스트캠퍼스&업스테이지 AI Lab 1기 (AI Lab 2기)  


## 기술 스택
- openai  
- elasticsearch  
- sentence_transformers 
- wandb
- gemini  


## 프로젝트 진행 단계  
1. 데이터 확인 및 데이터 전처리    
2. 전처리된 데이터를 모델에 적용 후 확인 및 평가    
3. 1번과 2번 반복  
4. 최종 제출  


## 프로젝트 세부 과정  
### 1. 데이터 확인 및 전처리  

**학습 데이터**  
과학 상식 문서 4272개  
ko_ai2_arc__ARC_Challenge와 ko_mmlu 데이터  
총 63개의 데이터 소스 (ko_mmlu__human_sexuality__train, ko_mmlu__human_sexuality__test 등을 별개로 카운트, 또한 ko_mmlu__human_sexuality__train과 ko_mmlu__conceptual_physics__train 도 별개로 카운트)  
파일 포맷은 각 line이 json 데이터인 jsonl 파일.  

질문 쿼리에 대한 정답이 없는 데이터
-> 정답 생성이 필요
+ 사람이 직접 정답 생성
+ LLM을 통하여 정답 생성

여기서는 과학 지식에 대한 도메인 지식이 부족기에 LLM을 이용해서 생성을 선택. 
개별 문서를 정답으로 보고, 이에 대한 질문을 생성하는 방식으로 수행.  


**평가 데이터**  
20개의 멀티턴 대화와 20개의 과학 상식 이외의 일상 대화  


### 3. 모델 선정  

Random Forest (RF), XGBoost (XGB), Light GBM (LGBM)  

XGB는 5-Fold와 optuna 사용시 시간이 너무 오래 소요되어 더 빠른 LGBM으로 선택후 고정  


### 4. 모델 적용 상세  
#### 4.1. 데이터 별 모델 적용  



#### 5. 최종 제출   
 


## 프로젝트 결과  
총 9개팀 참여  
Public 등수: 3등  
Private 등수: 4등  

Public Score: 18200.0390
Final(Public + Private) Score: 16173.2293

## 프로젝트 회고  
+ 초반 인덱스 문제로 인해서 리더보드와 Validation RMSE의 괴리가 심했다. 이때 Validation을 믿고 진행했어야 정상적으로 돌아온 리더보드에서 좋은 성능을 보였을 듯 하다. 다른 대회에 또 참여할 때 Validation을 믿고 실험을 수행해야겠다.
+ 실제 업무에서도 KPI의 설정은 정상적이더라도, 여러 이슈로 인해 성능 모니터링 대쉬보드 등이 잘못될 수 있다. 이를 유의해야겠다고 생각했다.
+ Kaggle이나 다른 레퍼런스를 추가로 찾아봤으면 좋았을듯하다.
+ 다른 팀원들과 토론하면서 인사이트를 얻을 수 있었고 각자 EDA나 수집한 데이터를 공유하여 시간을 아낄 수 있었다.
