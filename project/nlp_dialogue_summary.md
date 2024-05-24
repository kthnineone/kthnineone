# Dialogue Summarization | 일상 대화 요약 
## 프로젝트 개요
패스트캠퍼스&업스테이지 AI Lab 1기 자체 대회  

일상 대화를 바탕으로 요약문을 생성하는 모델을 구축함이 목적으로 회의, 일상 대화 등 다양한 주제를 가진 대화문과, 이에 대한 요약문을 포함

Puiblic과 Private은 각각 Random하게 5:5로 나뉜다.

평가 지표는 RMSE  

팀 프로젝트: 5명   
역할: EDA, 피쳐 엔지니어링, 모델링  
진행기간: 2024.01.07 ~ 2024.01.25  
소속 : 패스트캠퍼스&업스테이지 AI Lab 1기 (AI Lab 2기)  


## 기술 스택
+ Scikit-Learn
+ Numpy
+ Pandas
+ matplotlib
+ wandb
+ tqdm
+ pytorch_lightning
+ transformers[torch]
+ rouge

## 프로젝트 진행 단계  
1. 데이터 확인 및 데이터 전처리    
2. 전처리된 데이터를 모델에 적용 후 확인 및 평가    
3. 1번과 2번 반복  
4. 최종 제출  


## 프로젝트 세부 과정  
### 1. 데이터 확인 및 전처리  
연속형 변수: '전용면적', '계약년월', '계약일', '층', '건축년도', 'k-전체동수', 'k-전체세대수', 'target' 등등 총 18개  

범주형 변수: '시군구', '번지', '본번', '부번', '아파트명', '도로명', 'k-단지분류(아파트,주상복합등등)' 등등 총 34개  

- EasyDataAugmentation (EDA)
  - RandomDeletion (RD)
  - RandomInsertion (RI)
  - SynonymReplacement (SR)
  - RandomSwap (RS)
- AEasierDataAugmentation (AEDA)

```
from koeda import AEasierDataAugmentation
from koeda import EasyDataAugmentation

eda = EasyDataAugmentation(
              morpheme_analyzer = "Okt",
              alpha_sr = 0.1,
              alpha_ri = 0.1,
              alpha_rs = 0.1,
              prob_rd = 0.1
            )

repetition = 1

aeda = AEasierDataAugmentation(
        morpheme_analyzer="Okt", punctuations=[".", ",", "!", "?", ";", ":"]
    )

print("원문:", ex_data)
# First, apply EDA
result = eda(ex_data, repetition=repetition)
print("EDA:", result)
# Second, apply AEDA
result = aeda(ex_data, p=0.3, repetition=repetition)
print("AEDA:", result)
```


### 3. 모델 선정  

KoBART 

Text Summarization에는 Machine Reading Comprehension과
Text Generation 모두가 필요한 Encoder-Decoder 모델인 KoBART를 사용했습니다.

huggingface의 digit82/kobart-summarization.  


### 4. 모델 적용 상세  
#### 4.1. 데이터 별 모델 적용  



#### 5. 최종 제출   
 


## 프로젝트 결과  
총 9개팀 참여  
Public 등수: 8등  
Private 등수: 7등  

Public Score: 41.9246
Final(Public + Private) Score: 39.1958

## 프로젝트 회고  
+ 초반 인덱스 문제로 인해서 리더보드와 Validation RMSE의 괴리가 심했다. 이때 Validation을 믿고 진행했어야 정상적으로 돌아온 리더보드에서 좋은 성능을 보였을 듯 하다. 다른 대회에 또 참여할 때 Validation을 믿고 실험을 수행해야겠다.
+ 실제 업무에서도 KPI의 설정은 정상적이더라도, 여러 이슈로 인해 성능 모니터링 대쉬보드 등이 잘못될 수 있다. 이를 유의해야겠다고 생각했다.
+ Kaggle이나 다른 레퍼런스를 추가로 찾아봤으면 좋았을듯하다.
+ 다른 팀원들과 토론하면서 인사이트를 얻을 수 있었고 각자 EDA나 수집한 데이터를 공유하여 시간을 아낄 수 있었다.
