# 2008년 금융위기 이후 거시경제 측면에서 이자율이 투자에 미치는 영향  
## 프로젝트 개요
계량경제학 학기말 프로젝트  


평가 지표는 mAP (mean Average Precision)  

팀 프로젝트: 6명   
역할: 이론 및 아이디어, 가설 정립, R을 활용한 가설 구현  
진행기간: 2016.03 ~ 2016.06  
소속 : 연세대학교 


## 기술 스택
- R  
- R Studio  
- lmtest  
- ggplot2  


## 프로젝트 진행 단계  
1. 데이터 수집    
2. 회귀분석 시행    
3. Heteroskedasticity, Autocorrelation, Endogeneity, Multicollinearity의 4가지 회귀분석의 가정을 검정   
4. Heteroskedasticity, Autocorrelation 문제 발생
5. Cochrane-Orcutt Iterations로 Heteroskedasticity, Autocorrelation을 해결
6. Endogeneity 발생
7. Lagged Variable로 해결
8. 최종 가정 검정
9. 최종 회귀모형 선정
10. 결론  


## 프로젝트 세부 과정  
### 1. 데이터 수집  



### 2. 1차 회귀분석 시행  

Google의 Gemini 1.0으로 개별 과학 문서의 문서에서 생성가능한 질문 5개 생성  

### 3. 회귀분석의 가정 중 4가지를 검정 (test)   

 

#### 3.1. 검색 파트  
**Sparse Retrieval**  
Elasticsearch를 통해 BM25와 역색인으로 레퍼런스 목록 생성    


#### 3.2. LLM 생성 파트  

OpenAI의 ChatGPT 3.5와 4.0으로 답변 생성  

#### 3.3. 검색 파트  
**Sparse Retrieval**  
Elasticsearch를 통해 BM25와 역색인으로 레퍼런스 목록 생성    


#### 3.4. LLM 생성 파트  

OpenAI의 ChatGPT 3.5와 4.0으로 답변 생성  

### 4. 최종 회귀 모형 선정


### 5. 결론    
 


## 프로젝트 결과  


## 프로젝트 회고  
+ Elasticsearch 자체를 쓰는것도 좋지만 직접 구현하는 방법도 고려해볼 필요가 있다.
+ 쿼리가 과학상식인지 아닌지 구분하는 추가적인 별도의 모델을 둘 수도 있다.
 
