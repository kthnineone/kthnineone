# 네이버 웹툰 데이터를 활용한 미디어 믹스 예측  
## 프로젝트 개요

웹툰 소개, 장르, 연령등급 등을 활용하여 잠재적 미디어 믹스 대상 예측  
미디어 믹스란 웹툰을 애니메이션, 드라마, 영화 등으로 만들어 판매함을 의미한다.   

데이터 링크: [🔗](https://www.kaggle.com/datasets/0852b5bddaf671769494894556fee150c2bea66688548411446079f26eb2844c)
Project Jupyter Notebook link: [🔗 Details](https://github.com/kthnineone/kthnineone/blob/main/project/nlp_dialogue_summary.md)

개인 프로젝트   
역할: EDA, 피쳐 엔지니어링, 모델링  
진행기간: 2020.01 ~ 2020.02  
소속 : 없음


## 기술 스택
+ Scikit-Learn
+ Numpy
+ Pandas
+ matplotlib
+ wordcloud
+ gensim
+ transformers[torch]
+ konlpy


## 프로젝트 진행 단계  
1. 데이터 확인 및 데이터 전처리    
2. EDA로 탐색적 시각화      
3. 1번과 2번 반복  
4. 최종 제출  


## 프로젝트 세부 과정  
### 1. 데이터 확인 및 전처리  

### 2. EDA로 탐색적 시각화  

BarChart로 별점, 연령등급 비교  

BarChart와 wordcloud로 주요 장르 파악  

### 3. 모델 선정  

#### 1. Gensim - Word2Vec, FastText와 SVM으로 분류  

1. Gensim의 Word2Vec이나 FastTest로 문서를 임베딩화
2. SVM으로 분류하도록 학습 후 라벨 할당  
3. 테스트 데이터를 KNN으로 분류  

**성능**    
Accuracy: 0.8723404255319149


#### 2. Pre-Trained Model의 파인 튜닝을 활용한 분류  

1. KLUE 논문의 RoBERTa large model을 pre-trained model로 선정
2. KLUE의 토크나이저와 모델을 사용
3. 마지막 Classifier 모델만 학습하는 파인 튜닝 방식 채택
   이유는 데이터의 수가 적어서 언더피팅과 오버피팅의 가능성 모두 존재하기 때문.

**성능**  
Accuracy: 0.96509

### 4. 추가 분석: Topic Modeling  

주어진 genre에 대한 정보 없이 description만으로 장르에 따른 unsupervised clustering을 토픽 모델링으로 수행해보고 genre 별로 잘 분류되는지 확인이 목적  

1. Gensim의 LDA로 토픽 모델링 학습
2. 토픽은 6개로 선정  

목적도 다르고, 비지도 학습이기에 앞선 두 모델과 달리 Accuracy로 성능 비교가 불가.  
확인 결과 LDA를 이용하여 descprtion을 활용해 추가적인 장르에 대한 피쳐를 생성하는 것은 성능이 좋지 않음을 확인.  


## 프로젝트 결과  

+ Huggingface의 KLUE RoBERTa large model을 파인튜닝한 모델이 잠재적 미디어 믹스 예측에 있어서 더 좋은 성능을 보임.
+ 토픽 모델링을 활용한 description에서의 추가적인 장르 특성 파악은 도움이 되지 않았음.  
 

## 프로젝트 회고  
+ Desciption에 대한 정보를 보강하면 좋을것 같다.
+ 데이터를 더 많이 모을 수 있다면 좋을 듯 하다.  







https://github.com/kthnineone/code_notebook_archive/blob/main/Naver_Webtoon_NLP_Analysis.ipynb
