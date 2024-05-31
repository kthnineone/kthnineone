# Dialogue Summarization | 일상 대화 요약 
## 프로젝트 개요
패스트캠퍼스&업스테이지 AI Lab 1기 자체 대회  

일상 대화를 바탕으로 요약문을 생성하는 모델을 구축함이 목적으로 회의, 일상 대화 등 다양한 주제를 가진 대화문과, 이에 대한 요약문을 포함

Puiblic과 Private은 각각 Random하게 5:5로 나뉜다.

평가 지표는 ROGUE (Recall-Oriented Understudy for Gisting Evaluation)  


팀 프로젝트: 5명   
역할: EDA, 피쳐 엔지니어링, 모델링  
진행기간: 2024.03.08 ~ 2024.03.20  
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
+ koeda
+ rouge

## 프로젝트 진행 단계  
1. 데이터 확인 및 데이터 전처리    
2. 전처리된 데이터를 모델에 적용 후 확인 및 평가    
3. 1번과 2번 반복  
4. 최종 제출  


## 프로젝트 세부 과정  
### 1. 데이터 확인 및 전처리  

여러 명이 같이 대화하는 텍스트  
ROGUE-N의 측정방법으로 예측과 정답의 단어가 얼마나 겹치는 지를 평가한다.  
따라서 모델이 최대한 정답 그 자체를 그대로 생성하도록 학습한다.  
같은 뜻이지만 다른 문장을 생성하지 않는다.  

**텍스트 증강기법**  
EasyDataAugmentation (EDA)와 AEasierDataAugmentation (AEDA)  

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
Text Generation 모두가 필요한 Encoder-Decoder 모델인 KoBART를 사용  

huggingface의 digit82/kobart-summarization.  


#### 5. 최종 제출   
 


## 프로젝트 결과  
총 9개팀 참여  
Public 등수: 8등  
Private 등수: 7등  

Public Score: 41.9246
Final(Public + Private) Score: 39.1958

## 프로젝트 회고  
+ Wandb를 처음 사용해봤는데 굉장히 유용한 툴이라 앞으로도 자주 사용할 듯 싶다. 
+ EDA의 적용에 있어서 교착어인 한국어와 고립어인 영어는 형태소 분석이나 토크나이제이션 파트에서 다르게 적용해야 데이터 증강이나 성능의 향상에 있어서 유의미한 결과를 낼 수 있다.
+ Self-Attention, Encoder 구조, Decoder 구조 등 NLP 모델에 대한 이해와 더불어서 한국어가 지닌 고유의 언어학적 지식도 알아야 유의미한 결과를 낼 수 있으니 이에 유의해야겠다고 반성했다. 영어의 경우 형용사나 부사를 빼도 의미가 전달되는 경우가 있으나 한국어의 경우 조사 하나가 바뀌면 의미가 크게 바뀐다.
+ LLM 같은 거대한 모델은 개인이나 작은 규모의 기업, 연구집단에서는 파운데이션 모델을 건드리기 보다는 데이터에 집중해야 한다. 이는 곧 언어 자체에 대한 지식과, 그 언어가 사용되는 분야에 대한 이해, 예를 들어 전문문서 번역의 경우 의학이면 의학, 건설이면 건설분야에 대한 도메인 지식이 중요하다고 판단할 수 있다.
+ 다음에는 Backtranslation도 사용해봐야겠다. 특히 ROGUE 지표를 만족해야하므로 정답인 summary 보다는 dialogue에 증강을 적용하는게 좋아 보인다. 
+ Supervised Fine-Tuning Trainer랑 LORA도 사용해봐야겠다.
