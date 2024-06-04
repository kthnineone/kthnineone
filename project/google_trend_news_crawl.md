# 구글 트렌드와 뉴스 크롤링  
## 프로젝트 개요

+ 세계의 이슈를 알기 위해서 한국과 G7국가의 구글 트렌드 수집 (캐나다 제외)  
+ AI와 관련된 구글 뉴스 수집  

개인 프로젝트   
역할: 크롤러 개발 및 DB 형태로 저장  
진행기간: 2023.10.25 ~ 2023.10.31  
소속 : 패스트캠퍼스&업스테이지 AI Lab 1기 (AI Lab 2기)  


## 기술 스택
+ os
+ time
+ argparse
+ json
+ requests
+ selenium
+ googletrans
+ sqlite3
+ pandas

## 프로젝트 진행 단계  

1. 구글 트렌드 크롤링 구현  
2. 구글 뉴스 크롤링 구현  
3. 두 크롤러를 하나로 합침  
4. main 함수와 argparse를 활용하여 command로 구현.  
5. 구글 뉴스 크롤러가 동작하지 않아서 픽스  

## 프로젝트 세부 과정  
**구글 트렌드 크롤링**  

+ date, rank, title, content, search_count, crawltime을 저장  
+ 나라별로 별개의 table을 만들어서 저장한다.  
+ 일본, 프랑스, 독일, 이탈리아는 googletrans로 content 항목을 한국어와 영어 번역문을 추가하여
content_ko, content_en 항목으로 추가하여 저장
+ title의 경우 고유명사의 오역을 방지하기 위해 번역하지 않음.  

**구글 뉴스 크롤링**  
+ 키워드별로 별도의 테이블을 형성하여 저장
+ 테이블 이름이 경우 argparser로 별도로 지정한다.  


**main 함수화**
+ main 함수를 활용하여 .py 형태로 반환하여 command에서 작동시킴  
+ 크롤링이 완료되면 slack bot을 활용하여 알람을 보낸다.  

## 프로젝트 결과  


## 프로젝트 회고  
+ 크롤링한 내용을 토대로 wordcloud나 국가별 트렌드 비교, 시간차를 비교하면 인사이트를 얻을 수 있을듯 하다.  

