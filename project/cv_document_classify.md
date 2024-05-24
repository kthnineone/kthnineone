# Document Image Type Classification  
## 프로젝트 개요
패스트캠퍼스&업스테이지 AI Lab 1기 자체 대회  

다양한 종류의 문서 이미지를 입력 받아 17개의 클래스 중 정답을 예측하는 작업  

Puiblic과 Private은 각각 Random하게 5:5로 나뉜다.

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
+ Tensorboard  

## 프로젝트 진행 단계  
1. 데이터 확인 및 데이터 전처리    
2. 전처리된 데이터를 모델에 적용 후 확인 및 평가    
3. 1번과 2번 반복  
4. 최종 제출  


## 프로젝트 세부 과정  
### 1. 데이터 확인 및 전처리  
1570장의 학습 이미지를 통해 3140장의 평가 이미지를 예측
데이터가 어떤 class를 가지고 있는지 설명하는 meta.csv와 각 이미지 파일과 label을 매치한 train.csv 제공  

17개의 이미지 라벨 정보  
```  
0 계좌번호, 1 임신 의료비 지급 신청서, 2 자동차 계기판, 3 입·퇴원 확인서, 4 진단서, 5 운전면허증,
6 진료비 영수증, 7 외래 진료 증명서, 8 국민 신분증, 9 여권, 10 지불 확인서, 11 의약품 영수증, 12 처방전,
13 이력서, 14 의견 진술, 15 자동차 등록증, 16 자동차 등록판
```  

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


### 3. 모델 설명  

+ EfficientNet V2 M:  
Classifier만 학습하는 Transfer Learning과 전체를 학습하는 Fine-Tuning 모두 적용  

+ Two Stage Model:  
첫 번째 EfficientNet V2 M으로 자동차계기판, 자동차번호판, 문서를 분류. 두 번째 EfficientNet V2 M으로 나머지 15가지의 문서를 분류. 

### 4. 최종 제출   

다른 팀원의 모델 제출 (online and offline augmentation + stratified 5-fold)  
본인의 베스트 모델 성능은 Validaiton에 대해 0.9958, Public은 0.8110



## 프로젝트 결과  
총 9개팀 참여  
Public 등수: 7등  
Private 등수: 7등  

Public Score: 0.9303
Final(Public + Private) Score: 0.9183

## 프로젝트 회고  
+ Class Imbalance 문제를 해결할 때 Oversampling을 적용해볼 필요가 있었다.
+ Optimizer의 weight_decay나 lr scheduler 등을 적용해보지 못해서 아쉽다.
+ Train Loss과 Validation Loss가 똑같이 하락하고, Epochs도 30회 이내로 돌렸으나 리더보드와는 다른 결과가 나왔다. 따라서 오버피팅이 발생한 것으로 보여서 이를 해결하기 위한 방법이 필요하다. Mixup, Cutmix, 추가 Augmentations, 그리고 offline augmented images에 추가적으로 online augmentations 적용 등을 고려해볼만하다.  
+ 잘못된 라벨링 제거 혹은 수정 필요. 직접 찾거나 fastup을 이용.
+ 문서의 경우 제목만 crop한 경우도 존재한다.
+ 성능이 높았던 모델들을 앙상블하여 제출하는 방법도 고려해야 한다. TTA (Test Time Augmentation) 추가 공부 필요.
+ ViT 계열이나 EfficientNet B4, B7, Wide ResNet, CAFormer, MaxViT 등 다양한 모델의 실험도 고려해볼만하다.
+ Kaggle이나 다른 레퍼런스를 추가로 찾아봤으면 좋았을듯하다.
+ 다른 팀원들과 토론하면서 인사이트를 얻을 수 있었고 각자 EDA, Augmentations, 코드를 공유하여 시간을 아낄 수 있었다.
+ 멘토분을 통해 새로운 정보와 인사이트를 얻을 수 있었다. 추가적으로 살펴볼 모델과 논문들도 알게 되었다.
+ 보다 체계적으로 augmentations이나 현황에 대한 리뷰를 수행하고 이를 해결하기 위한 프로세스를 수행하지 못해서 아쉽다. 이를 보완해서 보다 메타적인 관점에서 문제와 현재 상황을 볼 필요가 있다.
