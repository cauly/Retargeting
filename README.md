Cauly 리타겟팅 연동 가이드
=========================
Mobile Web
--------------------------
### 개요
이 문서는 광고주가 Cauly 와 리타겟팅 연동을 할 때 광고주의 **모바일 WEB 페이지**에 tracker 를 삽입하는 방법에 대해서 설명하는 문서입니다.

### 문서 버전 
| 문서 버전 | 작성 날짜 | 작성자 및 내용|
 --- | --- | --- 
| 1.0.0 | 2016. 04. 05. | 권순국(nezy@fsn.co.kr) 초안 작성|
| 1.0.1 | 2016. 07. 14. | 권순국(nezy@fsn.co.kr) 문서 재정렬|


### 목차
- [연동 절차](#연동-절차)
- [연동 상세](#연동-상세) - 집행 예정인 캠페인 선택
  - [A. Feed 캠페인](#a-feed-캠페인)
  - [B. Static 캠페인](#b-static-캠페인)
  - [C. Install 캠페인](#c-install-캠페인)
- [페이지 별 설명](#페이지-별-설명)
	- [메인 페이지](#메인-페이지)
	- [상품 상세 페이지](#상품-상세-페이지)
	- [구매 완료 페이지](#구매-완료-페이지)
	- [전환 완료 페이지](#전환-완료-페이지)


### 연동 절차
1. Cauly 담당자 혹은 fsn_rt@fsn.co.kr로 연락하여 Cauly 리타겟팅 연동에 대해서 협의합니다.
1. 협의 완료 후, Cauly 담당자를 통해 track_code 를 발급받습니다.
1. track_code 를 포함한 tracker 코드를 아래 '연동상세'를 참고하여 해당하는 부분에 삽입합니다.
1. 코드 삽입 이후 연동이 되었는지 Cauly 에게 테스트를 요청합니다.
1. 테스트 완료 후 7일 뒤(주말 및 공휴일 포함) 광고 라이브 가능합니다.(단, 모수가 너무 적을 경우 모수 수집을 위해 추가 시간이 소요될 수 있습니다.)


### 연동 상세
Cauly 에서 발급한 track_code 를 aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 라고 가정하겠습니다.
예제 코드에서 aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 부분은 따로 발급 받은 track_code 로 대체하여야 합니다.

스크립트는 head 태그 보다는 body 태그 안쪽의 마지막 부분에 삽입하는 것이 좋습니다.

아래 3가지 캠페인 중 집행 예정인 캠페인에 맞게 tracker 스크립트를 삽입합니다.

#### A. Feed 캠페인
| 연동위치 | 목적 | 연동항목 | 연동 가이드 |
| ---------- | -------------- | ----------- | --------------- |
| 메인 페이지 | - 리타겟팅 광고 노출 대상자 선정 | 스크립트 삽입 | [바로 가기](#메인-페이지) |
| 상품 상세 페이지 | - 광고노출 대상자 별 추천 상품목록 생성<br/>- 상품이미지 및 정보를 광고 소재로 활용 | Meta 태그 삽입, 스크립트 삽입 | [바로 가기](#상품-상세-페이지) |
| 구매 완료 페이지 | - 추천상품에서 구매상품 제외 처리<br/>- ROAS 측정<br/>- 재구매율 측정(option) | 스크립트 삽입 | [바로 가기](#구매-완료-페이지) |

#### B. Static 캠페인
| 연동위치 | 목적 | 연동항목 | 연동 가이드 |
| ---------- | -------------- | ----------- | --------------- |
| 메인 페이지 또는 목적에 맞는 위치 | - 리타겟팅 광고 노출 대상자 선정 | 스크립트 삽입 | [바로 가기](#메인-페이지) |
| 전환 완료 페이지 | - 전환 건수 측정<br/>- 예) 상담신청완료 등 | 스크립트 삽입 | [바로 가기](#전환-완료-페이지) |

#### C. Install 캠페인
Install 캠페인과 함께 진행하는 캠페인(Feed 또는 Static) 연동 절차에 따라 연동한 후 추가로 아래 항목을 연동합니다.

| 연동위치 | 목적 | 연동항목 | 연동 가이드 |
| ---------- | -------------- | ----------- | --------------- |
| Android APP 마켓 | - Install 수 측정<br/>- Install 후 구매/전환 측정 | 앱연동 | [바로 가기](https://github.com/CaulyTracker/Android-Tracking-SDK-Hybrid) |

===

### 페이지 별 설명

#### 메인 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id','{$userId}']); // option
  _paq.push(['event_name','OPEN']);
  _paq.push(['age', "31"]); // option
  _paq.push(['gender', "M"]); // option
  _paq.push(['send_event']);
  (function()
  { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); })();
</script>
```


#### 상품 상세 페이지
###### meta 태그 삽입
상품 상세 페이지에 아래와 같은 meta 태그를 상품에 맞춰 추가해주어야 합니다.

```
<meta property="rb:type" content="product" />
<meta property="rb:cuid" content="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" />
<meta property="rb:itemId" content="{$itemId}" />
<meta property="rb:itemName" content="{$itemName}" />
<meta property="rb:itemImage" content="{$itemImage}" />
<meta property="rb:itemUrl" content="{$itemUrl}" />
<meta property="rb:originalPrice" content="{$originalPrice}" />
<meta property="rb:salePrice" content="{$salePrice}" />
<meta property="rb:category1" content="{$category1}" />
<meta property="rb:category2" content="{$category2}" />
<meta property="rb:category3" content="{$category3}" />
<meta property="rb:brandId" content="{$brandId}" />
<meta property="rb:brandName" content="{$brandName}" />
<meta property="rb:regDate" content="{$regDate}" />
<meta property="rb:updateDate" content="{$updateDate}" />
<meta property="rb:stock" content="{$stock}" />
<meta property="rb:state" content="{$state}" />
<meta property="rb:description" content="{$description}" />
<meta property="rb:extraImage" content="{$extraImage}" />
<meta property="rb:locale" content="{$locale}" />
```

Nullable의 Not NULL은 필수로 채워야 하는 값이며, 필수가 아닌 옵션 값들은 NULL로 표시되었습니다. 옵션 항목은 값이 비어 있더라도 태그 자체는 존재해야 합니다.

| Field Name | Java Data Type | Column Name | MySql Data Type | Nullable | E-commerce Description | media Description |
| ---------- | -------------- | ----------- | --------------- | -------- | ---------------------- | ----------------- |
| itemId | String | item_id | varchar(100) | NOT NULL | 상품ID | 컨텐츠 ID |
| itemName | String | item_name | varchar(500) | NOT NULL | 상품명 | 컨텐츠 제목 |
| itemImage | String | item_image | text | NOT NULL | 상품 이미지 URL | 컨텐츠 이미지 URL |
| originalPrice | double | original_price | decimal(16,6) | NOT NULL | 제품가격 | - |
| salePrice | double | sale_price | decimal(16,6) | NOT NULL | 판매가격 | - |
| category1 | String | category1 | varchar(50) | NOT NULL | 카테고리 (대) <br/>ex) 의류, 스포츠, 가구 | 섹션 (대) |
| category2 | String | category2 | varchar(50) | NOT NULL | 카테고리 (중) <br/>ex) 여성의류, 등산, 주방가구 | 섹션 (중) |
| category3 | String | category3 | varchar(50) | NULL | 카테고리 (소) | 섹션 (소) |
| category4 | String | category4 | varchar(50) | NULL | 카테고리 (세) | 섹션 (세) |
| category5 | String | category5 | varchar(50) | NULL | 카테고리 (세세) | 섹션 (세세) |
| itemUrl | String | item_url | text | NULL | 상품 landing URL | 컨텐츠 landing URL |
| brandId | String | brand_id | varchar(100) | NULL | 브랜드 ID | - |
| brandName | String | brand_name | varchar(500) | NULL | 브랜드명 | - |
| regDate | String | reg_date | datetime | NULL | 상품 등록일 <br/>ex) 2015-06-25T05:43:18Z | 컨텐츠 게재일|
| updateDate | String | update_date | datetime | NULL | 상품 갱신일 <br/>ex) 2015-06-25T05:43:18Z | 컨텐츠 변경일 |
| expireDate | String | expire_date | datetime | NULL | 상품 만료일 <br/>ex) 2015-06-25T05:43:18Z | 컨텐츠 만료일 |
| stock | int | stock | int | NULL | 재고 | - |
| state | String | state | varchar(100) | NULL | 상품 상태 기술 필드. e.g., available, soldout, ... 추천에서 제거하고 싶을 때는 REC_EXCLUDE 로 명시| - |
| description | String | description | Sttext | NULL | 상품 설명 | 컨텐츠 내용 |
| extraImage | String | extra_image | text | NULL | 상품 추가 이미지. 다수의 이미지 가능. 필드 구분자로 구분. | 컨텐츠 추가 이미지 |
| locale | String | locale | varchar(20) | NULL | 지역 코드. 화폐나 상품명이 적용받음. <br/>e.g., KR, US, ... | 컨텐츠 지역 코드 |

###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id','{$userId}']); // option
  _paq.push(['event_name','PRODUCT']);
  _paq.push(['event_param','{$itemId}']);
  _paq.push(['send_event']);
  (function() { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
)();
</script>
```
| Field Name | Nullable | Description | 
| ---------- | -------- | ----------- |
| {$itemId} | NOT NULL | 현재 방문한 상품의 아이디, 고객사의 상품ID(상품코드)를 넣는다. |
| {$userId} | NULL | 방문한 유저의 로그인 아이디 (optional) 법적이슈의 문제로 HASH 값을 넣어주는 것이 일반적이다. |


#### 구매 완료 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id','{$userId}']); // option
  _paq.push(['event_name','PURCHASE']);
  _paq.push(['order_id','{$orderId}']);
  _paq.push(['order_price','{$orderPrice}']);
  var products_q = [];

  /* STAR LOOP: 구매한 모든 상품에 대해 */
  products_q.push({'product_id': '{$itemId}','product_price':'{$productPrice}','product_quantity':'{$productQuantity}'});
  /* END LOOP */

  _paq.push(['product_infos',products_q]);
  _paq.push(['send_event']);    
  (function(){ var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
)();
</script>
```
| Field Name | Nullable | Description | 
| ---------- | -------- | ----------- |
| {$itemId} | NOT NULL | 결제된 상품 ID (상품코드). <br/>이때의 상품ID는 상품상세 페이지에서 전달한 상품ID와 동일한 것이어야 한다. |
| {$productPrice} | NOT NULL | 결제된 개별 상품들의 가격 |
| {$productQuantity} | NOT NULL | 결제된 상품의 갯수 |
| {$orderId} | NOT NULL | 결제완료된 주문 ID |
| {$orderPrice} | NOT NULL | 결제완료된 주문 ID 기준의 주문가격, 전체 금액 |
| {$userId} | NULL | 방문한 유저의 로그인 아이디 (optional) 법적이슈의 문제로<br/> HASH 값을 넣어주는 것이 일반적이다. |


###### 스크립트 삽입(재구매를 따로 표시하고 싶은 경우)
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id','{$userId}']); // option
  _paq.push(['event_name','PURCHASE']);
  _paq.push(['order_id','{$orderId}']);
  _paq.push(['order_price','{$orderPrice}']);
  /* 재구매 표시 시작, 재구매 표시를 위해 이 부분이 추가되었다. */
  _paq.push(['purchase_type', 'RE-PURCHASE']);
  /* 재구매 표시 끝 */
  var products_q = [];

  /* STAR LOOP: 구매한 모든 상품에 대해 */
  products_q.push({'product_id': '{$itemId}','product_price':'{$productPrice}','product_quantity':'{$productQuantity}'});
  /* END LOOP */

  _paq.push(['product_infos',products_q]);
  _paq.push(['send_event']);    
  (function(){ var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
)();
</script>
```

#### 전환 완료 페이지
###### 스크립트 삽입
```javascript
<script type="text/javascript">
  window._paq = window._paq || [];
  _paq.push(['track_code',"aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"]);
  _paq.push(['user_id','{$userId}']); // option
  _paq.push(['event_name','CA_CONVERSION']);
  _paq.push(['send_event']);
  (function() { var u="//image.cauly.co.kr/script/"; var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0]; g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'caulytracker_async.js'; s.parentNode.insertBefore(g,s); }
  )();
</script>
```

event
- CA_CONVERSION: 전환 체크
- CA_*: CA_APPLY, CA_REGISTER 등으로 사용할 수도 있으나 기능 상의 차이는 없습니다.
