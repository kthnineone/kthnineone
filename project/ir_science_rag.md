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
### 1. 데이터 확인  

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


### 2. 데이터 전처리  

Google의 Gemini 1.0으로 개별 과학 문서의 문서에서 생성가능한 질문 5개 생성  

### 3. 모델   

![image](https://github.com/kthnineone/kthnineone/blob/main/images/rag_structure_edited.png)  

검색을 이용해서 쿼리에 대한 레퍼런스 목록 생성  
이를 바탕으로 쿼리와 함께 LLM으로 답변 생성  

#### 3.1. 검색 파트  
**Sparse Retrieval**  
Elasticsearch를 통해 BM25와 역색인으로 레퍼런스 목록 생성    

**Dense Retrieval**  
sentence_transformers의 "snunlp/KR-SBERT-V40K-klueNLI-augSTS"의 encode로 문서 임베딩 생성 후 유사한 KNN으로 레퍼런스 목록 생성  

#### 3.2. LLM 생성 파트  

OpenAI의 ChatGPT 3.5와 4.0으로 답변 생성  

Role과 Instructions를 활용하여 LLM에게 명확하게 명령한다.  


#### 5. 최종 제출   
 


## 프로젝트 결과  
총 3개팀 참여  
Public 등수: 3등  
Private 등수: 3등  

Public Score: 0.7076
Final(Public + Private) Score: 0/7152

## 프로젝트 회고  
+ Elasticsearch 자체를 쓰는것도 좋지만 직접 구현하는 방법도 고려해볼 필요가 있다.
+ 쿼리가 과학상식인지 아닌지 구분하는 추가적인 별도의 모델을 둘 수도 있다.
+ Elasticsearch에 쓰인 역색인이나 BM25를 건드리는 대신 동의어, 유의어 처리, 토크나이저 등의 변경 등이 더 중요하다. 데이터의 품질에 집중하는게 좋다.
+ 같은 모델이라도 seed를 변경하는 방법도 고려해볼만했는데 적용하지 못해서 아쉬웠다. 
+ 멘토님이 질의와 응답에 대한 hard negative pairs를 생성하라고 조언해주셨다. 이는 똑같은 물리학이라도 전자기학과 양자역학이 서로 다르기 때문에, 커다랗게는 같은 도메인일지라도 세부 내용을 달리하여 보다 섬세하게 학습을 할 수 있도록 한다. 하지만 이는 사람이 수작업으로 매칭을 해야하고 도메인 지식이 많이 요구되기 때문에 수행할 수 없었다.
+ Sentence Transformer이 아닌 Huggingface의 모델을 파인 튜닝 후 적용하지 못해서 아쉬웠다.
+ 유저 사전을 만들어서 konlpy와 huggingface 모델에는 등록을 해봤으나 sentence_transformer에는 적용하고 실제 LLM 생성까지 이어지지 못해서 아쉽다.
+ '통학 버스의 가치에 대해 말해줘.'와 같이, 교육과 관련된 내용인지 교통공학에 관련된 내용인지,
  그리고 버스라는 자체로 기계공학이나 전자공학과 관련된 내용인지 애매한 항목에 대한 추가적인 분석이 부족했다.
+ 다들 IR분야에 생소하기도 하고 Elasticsearch를 처음 사용해서 문서 자체에 대한 언어적, 도메인적 분석을 충분히 하지 못한 점이 아쉽다. 
+ 구체적인 질의 내용이 아닌 내용들을 레퍼런스로 삼아서 LLM이 정답을 생성했기 때문에 점수가 낮았다.
  예를 들어 "나무 분류"에 대해서 알려달라한 질문에 대해서 "나무 분류"랑 상관없는 나무 내용들이 높은 점수를 얻은 레페런스가 되었다. LLM의 생성 결과에 대한 분석을 시간 부족으로 인해 하지 못해서 아쉽다.  
