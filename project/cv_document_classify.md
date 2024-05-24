# Document Image Type Classification  
## 프로젝트 개요
패스트캠퍼스&업스테이지 AI Lab 1기 자체 대회  

다양한 종류의 문서 이미지를 입력 받아 17개의 클래스 중 정답을 예측하는 작업  

Puiblic과 Private은 각각 Random하게 5:5로 나뉜다.

추가 데이터로 지하철역, 버스정류장 정보 등이 존재  

평가 지표는 Macro F1  

팀 프로젝트: 5명   
역할: EDA, 피쳐 엔지니어링, 모델링  
진행기간: 2024.01.07 ~ 2024.01.25  
소속 : 패스트캠퍼스&업스테이지 AI Lab 1기 (AI Lab 2기)  


## 기술 스택
+ Scikit-Learn
+ Numpy
+ Pandas
+ matplotlib
+ albumentations
+ PyTorch

## 프로젝트 진행 단계  
1. 데이터 확인 및 데이터 전처리    
2. 전처리된 데이터를 모델에 적용 후 확인 및 평가    
3. 1번과 2번 반복  
4. 최종 제출  


## 프로젝트 세부 과정  
### 1. 데이터 확인 및 전처리  
1570장의 학습 이미지를 통해 3140장의 평가 이미지를 예측
데이터가 어떤 class를 가지고 있는지 설명하는 meta.csv와 각 이미지 파일과 label을 매치한 train.csv 제공  

```0 계좌번호, 1 임신 의료비 지급 신청서, 2 자동차 계기판, 3 입·퇴원 확인서, 4 진단서, 5 운전면허증,
6 진료비 영수증, 7 외래 진료 증명서, 8 국민 신분증, 9 여권, 10 지불 확인서, 11 의약품 영수증, 12 처방전,
13 이력서, 14 의견 진술, 15 자동차 등록증, 16 자동차 등록판```

car_dashboard와 vehicle_registration_plate가 이질적, 나머지 classes의 이미지는 모두 문서의 형태

test data는 flip, rotate, mixup 등이 되어 있는 문서 이미지

**16 Offline Augmentations:**  
다양하게 변형된 features를 학습하여 robust한 모델을 만들기 위해 offline 방법 적용.


+ HorizontalFlip
+ VerticalFlip
+ ShiftScaleRotate
+ Grayscale
+ ColorJitter
+ Blur
+ MedianBlur
+ Spatter
+ Defocus
+ ZoomBlur
+ OpticalDistortion 2장
+ Perspective 2장
+ Rotate 2장

### 2. EDA

+ labeling이 애매한 데이터들 존재
+ 대부분의 모델이 3, 7, 13번 class를 자주 혼동하는 경향을 보임
+ Scikit-Learn의 Confusion Matrix의 시각화로 잘 분류되는 클래스와 자주 혼동되는 클래스 확인


### 3. 모델 선정  

EfficientNet V2 M:
Classifier만 학습하는 Transfer Learning과 전체를 학습하는 Fine-Tuning 모두 적용
Two Stage Model:
첫 번째 EfficientNet V2 M으로 자동차계기판, 자동차번호판, 문서를 분류. 두 번째 EfficientNet V2 M으로 나머지 15가지의 문서를 분류. 


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
