# 알라딘 챗봇

챗봇 시스템 개발 프로젝트
![파일 링크 첨부](https://drive.google.com/drive/folders/1LUAE4Ys2xRR97l9uNGyd2PM8hU6lI_Zw?usp=drive_link)
<br>

## 배경/목적
중고서적의 경우 파는 매장이 한정되어있고, 매장마다 보유하고 있는 서적이 다름 

또한 책을 매장별로 따로 살 경우 배송비가 증가함

때문에 구매 리스트의 책을 가장 많이 겹치게 보유한 매장을 수작업으로 찾는 불편함이 있었음 

이에 평소 알라딘 중고매장 사용시 필요성을 느낀 기능 구현하고자 함

<br>

## 기능 정의
- **책 추천 기능**
  - 검색한 책과 비슷한 지식을 담고 있는 책 추천
    
- **중고상품 보유 매장 검색**
  - 검색한 책을 보유하고 있는 매장 파악
  - 현황 바탕으로 구매 매장 추천

<br>

 ![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/0d6382e7-5427-4b8b-8af4-c7e37bba6ae9)

<br>

> CategoryID 분야의 고유번호, Description 상품설명(요약) ,authors 참여작가/아티스트 정보 등을
> 
> 종합적으로 고려한 책 추천 알고리즘 기능 구현

<br>

![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/556af855-dbf7-472d-b0ca-d5319814d7b5)

<br>

> 알라딘 중고서점에서 책을 검색하면 특정 지점에서만 재고가 있는 것을 확인 할 수 있음.
> 
> 예를 들어 위와 같은 경우 두 책을 각기 다른 지점에서 배송 주문을 하면 배송료를 각 지점에 각각 지불해야하는 상황이 생김.
> 
> 따라서, 사고 싶은 몇몇 책을 선택 했을 때 두 책을 공통으로 가지고 있는 중고서점을 찾아주는 기능 구현

<br>

ex) user :국가는 왜 실패하는가하고 예술과 영혼을 사고싶어

chatbot : 동탄2하나로마트점은 두 책을 동시에 보유하고 있어요

![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/8975398b-dc40-477e-b5ea-43ed679d0985)

<br>

## 구현 계획
### 챗봇 절차
![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/71257bc4-bce7-46b3-be2f-4fac3c75598e)
![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/0882e801-aaee-4b33-b808-d0e42759ad7b)
![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/5351ad0f-9b12-4353-a268-8636d537f306)

### 알라딘 Open API
#### 1. 상품 검색/상품 리스트/상품 조회 API

**1) 요청**

URL : http://www.aladin.co.kr/ttb/api/ItemSearch.asp

URL샘플

http://www.aladin.co.kr/ttb/api/ItemSearch.aspx?ttbkey=[TTBKey]&Query=aladdin&QueryType=Title&MaxResults=10&start=1&SearchTarget=Book&output=xml&Version=20131101

![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/eb0ab950-f3c4-4743-b32e-2bad5876b977)

**2) 응답**

![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/6391586a-fcc3-4688-bd5b-be4e82902abf)

<br>

#### 2. 중고상품 보유 매장 검색 API

**1) 요청**

URL: http://www.aladin.co.kr/ttb/api/ItemOffStoreList.aspx

URL샘플

http://www.aladin.co.kr/ttb/api/ItemOffStoreList.aspx?ttbkey=[TTBKey]&itemIdType=ISBN&ItemId=[도서
의ISBN]&output=xml

![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/6c48c2ea-1c80-4cad-9965-9d4bb70e6ec3)

**2) 응답**

![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/6f888f43-d1f5-46fd-84bb-ce9ba7113d53)

> 상품 검색 api에 parameter 중 Query를 keyword로 두고
>
> title customerReviewRank salesPoint isbn을 추출해 내어
>
> customerReviewRank와 salesPoint의 가중치 합(현재 salesPoint만 고려) 순으로 정렬
>
> 책을 보유하고 있는 중고 매장이 존재할 때만 책 이름과 매장 이름을 저장한다. 이후 함수에서 활용

<br>

#### 함수
![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/f69a1ad5-db93-4bc8-af09-0a583c7ed6c0)


## GUI
![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/314efbb2-2640-41af-9289-ac48698f3b98)
![image](https://github.com/AI-School-Avengers/ChatBot/assets/37794363/1a6d5ebd-7062-4847-be73-97fed563e493)

## 시연 영상




https://github.com/AI-School-Avengers/ChatBot/assets/37794363/94ebc948-4b2c-44c6-b297-4ee50a5e6cb6

