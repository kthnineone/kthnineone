# 공공 데이터를 활용한 제주도 관광 개발 및 홍보 방향 제시  
## 프로젝트 개요

  공공데이터를 활용한 시각화를 통해 제주도 방문객 파악 및 관광 상품 개발 및 홍보 방향 제시

팀 프로젝트: 3명   
역할: EDA  
진행기간: 2023.11.06 ~ 2023.11.15  
소속 : 패스트캠퍼스&업스테이지 AI Lab 1기 (AI Lab 2기)  


## 기술 스택
+ os
+ time
+ pandas
+ matplotlib
+ seaborn
+ plotly
+ geopandas
+ folium

## 프로젝트 진행 단계  

1. 각자 EDA 수행
2. EDA로 얻은 인사이트 공유
3. EDA를 통한 제주 관광 현황 확인
4. 현황에 기반한 관광 발전 방향 논의 및 결론도출  


## 프로젝트 세부 과정  

여러가지 차트들; Bar Chart, Area Chart, Time Series Chart, Treemap, Heatmap를 활용해 인사이트 추출  

Stacked Bar Chart  
![image](https://github.com/kthnineone/kthnineone/blob/main/images/Monthly_visitor_Count_Stacked_Bar_Chart_matplotlib.png)  



Area Chart  
![image](https://github.com/kthnineone/kthnineone/blob/main/images/Monthly_visitor_Count_Area_Chart_plotly.png)  


Time Series Chart  

![image](https://github.com/kthnineone/kthnineone/blob/main/images/Monthly_visitor_Count_TimeSeries_plotly.png)  


Hierearchical Treemap  

![image](https://github.com/kthnineone/kthnineone/blob/main/images/Monthly_Treemap_and_Nation_Proportion.png)  


Heatmap  

![image](https://github.com/kthnineone/kthnineone/blob/main/images/Monthly_Heatmap_and_Nation_Log_Raw_Count.png) 


중국, 일본, 대만, 미국, 홍콩이 한국 방문 상위권 국가들이다.  

+ 방문 목적별로 Treemap을 그려서 확인한 결과  
  여행이 목적인 경우는 중국, 일본, 대만, 미국이 상위권이다.  
  비즈니스가 목적인 경우는 중국, 인도, 일본, 베트남이 상위권이다.  
  공무가 목적인 경우는 미국, 중국, 베트남, 몽골, 태국이 상위권이다.  
  그외 방문 목적인 경우 중국, 필리핀, 미국, 해외 교포가 상위권이다.  
  
+ 제주도 입도 외국인 수의 경우 중국이 압도적으로 1위고, 미국, 일본, 대만이 상위권이다.  

읍면동별 국가별 방문자 수  

![image](https://github.com/kthnineone/kthnineone/blob/main/images/jeju_dong_visitor_by_nation_treemap.png) 

![image](https://github.com/kthnineone/kthnineone/blob/main/images/jeju_dong_visitor_by_nation.PNG)  

**(지도 시각화의 경우 팀원의 수행 결과물)**  

+ 인기 있는 읍면동의 경우 대체로 자연, 액티비티, 문화를 즐길 수 있는 지역들이다.  



## 프로젝트 결과  

제주 관광 상품 제작 및 홍보 방안 제시  

+ 제주도의 핵심 여행 자원은 자연, 액티비티, 문화다.  
+ 오름과 같은 고유의 자연 환경이 매력적인 지역들의 경우 난개발을 막고 자연을 보존해야 한다.
+ 중국 관광객이 많기 때문에 관련된 지원을 강화해야 한다.
+ 오름이나 제주 민속촌의 경우 태국과 말레이시아 관광객이 많이 찾기에 언어적 지원이나 가이드를 늘리거나 홍보를 강화해야 한다.  


## 프로젝트 회고  
+ 팀원이 geopandas와 folium을 활용하여 지도 시각화를 수행하였는데 이를 나중에 활용해봐야겠다.
+ plotly는 dash와 연계하여 대쉬보드를 만들 수도 있는데 이렇게 발전시켜 보는 방향도 고려할만하다.  



