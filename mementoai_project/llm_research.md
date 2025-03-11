# LLM 모델 연구  
## 프로젝트 개요

10 B 이하의 새로운 아키텍처를 가진 LLM 개발이 목적  
T5와 Recurrent Gemma를 기반으로 개선 시도  


팀 프로젝트: 2명   
역할: 데이터 수집, 데이터 전처리, 벤치마크 리서치, 모델 아키텍처 구성, 실험      
진행기간: 2024.10.02 ~ 2025.01.10  
소속 : 메멘토에이아이   


## 기술 스택  
+ Numpy  
+ Pandas  
+ PyTorch  
+ Huggingface  
+ Multi-GPU Parallel Computing  
+ Wandb  


## 프로젝트 진행 단계  
1. Recurrent Gemma, Nano GPT 등의 레퍼런스 확인       
2. 아이디어 회의    
3. 학습을 위한 데이터 및 성능 레퍼런스 리서치  
4. 학습을 위한 데이터 전처리         
5. T5 모델 성능 reproduce 시도  
6. T5를 기반으로 한 새로운 구조의 모델 학습  
7. 회사 폐업으로 중단       



## 프로젝트 회고  
+ Andej Karpathy의 [Nano GPT](https://github.com/karpathy/nanoGPT)를 기반하여 학습  
+ Multi-GPU Parallel Computing를 PyTorch의 DistributedDataParallel(DDP)로 구현  
+ Model 자체를 나눠서 담는 기술인 Fully Sharded Data Parallel (FSDP) 적용 필요  
+ Screen과 logging, wandb로 모니터링  
+ LangChain 등의 기술을 사용하지 못함   
+ Domain Specific Model 개발까지 기획했으나 실행하지 못함 
