Cauly 리타겟팅 연동 가이드
=========================
광고주 Web - with Recobell
--------------------------
### 개요
이 문서는 광고주가 Cauly 와 feed 형 리타겟팅 연동을 할 때 tracker 를 삽입하는 방법에 대해서 설명하는 문서입니다.

### 문서 버전 
| 문서 버전 | 작성 날짜 | 작성자 및 내용|
 --- | --- | --- 
| 1.0.0 | 2016. 04. 05. | 권순국(nezy@fsn.co.kr) 초안 작성|



### 목차
- [연동 절차](#연동-절차)
- [연동 상세](#연동-상세)
	- [메인 페이지](#메인-페이지)
		- 스크립트 삽입
	- [상품 상세 페이지](#상품-상세-페이지)
		- [meta 태그 삽입](#meta-태그-삽입)
		- 스크립트 삽입
	- [구매 완료 페이지](#구매-완료-페이지)
		- 스크립트 삽입


### 연동 절차
Cauly 담당자 혹은 cauly@fsn.co.kr로 연락하여 Cauly 리타겟팅 연동에 대해서 협의합니다.
협의 완료 후, site_code 를 발급받습니다.
site_code 를 포함한 tracker 코드를 사이트의 각 페이지에 삽입합니다.
페이지 삽입 이후 연동이 되었는지 Cauly 에서 테스트를 진행합니다.
테스트가 완료되면 광고를 집행합니다.


### 연동 상세
tracker 스크립트의 삽입 위치는 아래 3군데이며 차례대로 기술하겠습니다.
- 메인 페이지
- 상품 상세 페이지
- 구매완료 페이지

Cauly 에서 발급한 track_code 를 aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 라고 가정하겠습니다.
예제 코드에서 aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee 부분은 따로 발급 받은 track_code 로 대체하여야 합니다.

### Native SDK
1.0.1 버전 iOS/Android SDK의 Purchase API는 작동하지 않습니다.
- [Android SDK](https://github.com/CaulyTracker/Android-Tracking-SDK)
- [iOS SDK](https://github.com/CaulyTracker/iOS-Tracking-SDK)

#### 메인 페이지
##### 스크립트 삽입
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
        var mTracker = new CaulyTracker();
        var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
         mTracker.init(initData);
         mTracker.trackEvent('OPEN');  
</script>
```

스크립트는 <head> 보다는 <body> 태그 안쪽의 마지막 부분에 삽입하는 것이 좋습니다.


#### 상품 상세 페이지
##### meta 태그 삽입
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

빨간색으로 표시된 값들은 필수로 채워야 하는 값이며, 필수가 아닌 옵션 값들은 초록색으로 표시되었습니다. 옵션 항목은 값이 비어 있더라도 태그 자체는 존재해야 합니다.

| Field Name | Java Data Type | Column Name | MySql Data Type | Nullable | E-commerce Description | media Description |
| ---------- | -------------- | ----------- | --------------- | -------- | ---------------------- | ----------------- |
| itemId | String | item_id | varchar(100) | NOT NULL | 상품ID | 컨텐츠 ID |
| itemName | String | item_name | varchar(500) | NOT NULL | 상품명 | 컨텐츠 제목 |
| itemImage | String | item_image | text | NULL | 상품 이미지 URL | 컨텐츠 이미지 URL |
| itemUrl | String | item_url | text | NULL | 상품 ladning URL | 컨텐츠 landing URL |
| originalPrice | double | original_price | decimal(16,6) | NOT NULL | 제품가격 | - |
| salePrice | double | sale_price | decimal(16,6) | NOT NULL | 판매가격 | - |
| category1 | String | category1 | varchar(50) | NOT NULL | 카테고리 (대) | 섹션 (대) |
| category2 | String | category2 | varchar(50) | NOT NULL | 카테고리 (중) | 섹션 (중) |
| category3 | String | category3 | varchar(50) | NULL | 카테고리 (소) | 섹션 (소) |
| category4 | String | category4 | varchar(50) | NULL | 카테고리 (세) | 섹션 (세) |
| category5 | String | category5 | varchar(50) | NULL | 카테고리 (세세) | 섹션 (세세) |
| brandId | String | brand_id | varchar(100) | NULL | 브랜드 ID | - |
| brandName | String | brand_name | varchar(500) | NULL | 브랜드명 | - |
| regDate | String | reg_date | datetime | NULL | 상품 등록일, ex) 2015-06-25T05:43:18Z | 컨텐츠 게재일|
| updateDate | String | update_date | datetime | NULL | 상품 갱신일, ex) 2015-06-25T05:43:18Z | 컨텐츠 변경일 |
| expireDate |  | String | expire_date | datetime | NULL | 상품 만료일, ex) 2015-06-25T05:43:18Z | 컨텐츠 만료일 |
| stock | int | stock | int | NULL | 재고 | - |
| state | String | state | varchar(100) | NULL | 상품 상태 기술 필드. e.g., available, soldout, ... | - |
| description | String | description | Sttext | NULL | 상품 설명 | 컨텐츠 내용 |
| extraImage | String | extra_image | text | NULL | 상품 추가 이미지. 다수의 이미지 가능. 필드 구분자로 구분. | 컨텐츠 추가 이미지 |
| locale | String | locale | varchar(20) | NULL | 지역 코드. 화폐나 상품명이 적용받음. e.g., KR, US, ... | 컨텐츠 지역 코드 |

##### 스크립트 삽입
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
        var mTracker = new CaulyTracker();
        var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
         mTracker.init(initData);
         mTracker.trackEvent('PRODUCT');  
</script>

<script type="text/javascript">
  var _rblqueue = _rblqueue || [];
  _rblqueue.push(['setVar','cuid','aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee']);
  _rblqueue.push(['setVar','device','{$device}']);
  _rblqueue.push(['setVar','itemId','{$itemId}']);
  _rblqueue.push(['setVar','userId','{$userId}']);		// optional, should be less than 80 char
  _rblqueue.push(['setVar','searchTerm','{$searchTerm}']);  
  _rblqueue.push(['track','view']);
  _rblqueue.push(['track','product']);  /* -- IMPORTANT -- */
  setTimeout(function() {
    (function(s,x){s=document.createElement('script');s.type='text/javascript';
    s.async=true;s.defer=true;s.src=(('https:'==document.location.protocol)?'https':'http')+
    '://assets.recobell.io/rblc/js/rblc-apne1.min.js';
    x=document.getElementsByTagName('script')[0];x.parentNode.insertBefore(s, x);})();
  }, 0);
</script>
```

- {$device} : 현재 방문한 페이지의 분류. 아래 4가지 값 중 하나를 가져야 한다.
 - PW : PC Web
 - MW : Mobile Web
 - MI : Mobile iOS
 - MA : Mobile Android
- {$itemId} : 현재 방문한 상품의 아이디, 고객사의 상품ID(상품코드)를 넣는다.
- {$userId} : 방문한 유저의 로그인 아이디 (optional) 법적이슈의 문제로 HASH 값을 넣어주는 것이 일반적이다.
- {$searchTerm} : 사이트 내부에서 검색을 통해서 상품상세 페이지로 들어왔다면, 검색어를 넣는다. 상품 상세 페이지에서 검색어를 얻을 수 없다면 비워두면 된다.


#### 구매 완료 페이지
##### 스크립트 삽입
```javascript
<script type="text/javascript" src="//image.cauly.co.kr/script/caulytracker.js"></script>
<script type="text/javascript">
         var mTracker = new CaulyTracker();
         var initData = mTracker.InfoBuilder.setTrackCode("aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee").build();
          mTracker.init(initData);

          /* STAR LOOP: 구매한 모든 상품에 대해 */
          mTracker.PurchaseEvent.addPurchase( "{$itemId}", "{$productPrice}", "{$productQuantity}");
          /* END LOOP */

          mTracker.PurchaseEvent.setOrder("{$orderId}", "{$orderPrice}");

          var purchaseEvent = mTracker.PurchaseEvent.build();
          mTracker.trackEvent(purchaseEvent);
</script>

<script type="text/javascript">
  var _rblqueue = _rblqueue || [];
  /* STAR LOOP: 구매한 모든 상품에 대해 */
  _rblqueue.push(['addVar', 'orderItems', {itemId:'{$itemId}', price:'{$productPrice}', quantity:'{$productQuantity}'}]);
  /* END LOOP */
</script>

<script type="text/javascript">
var _rblqueue = _rblqueue || [];
_rblqueue.push(['setVar','cuid','aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee']);
_rblqueue.push(['setVar','device','{$device}']);
_rblqueue.push(['setVar','orderId','{$orderId}']);
_rblqueue.push(['setVar','orderPrice','{$orderPrice}']);
_rblqueue.push(['setVar','userId','{$userId}']);		// optional
_rblqueue.push(['track','order']);
setTimeout(function() {
  (function(s,x){s=document.createElement('script');s.type='text/javascript';
  s.async=true;s.defer=true;s.src=(('https:'==document.location.protocol)?'https':'http')+
    '://assets.recobell.io/rblc/js/rblc-apne1.min.js';
  x=document.getElementsByTagName('script')[0];x.parentNode.insertBefore(s, x);})();
}, 0);
</script>
```


- {$itemId} : 결제된 상품 ID (상품코드). 이때의 상품ID는 상품상세 페이지에서 전달한 상품ID와 동일한 것이어야 한다.
- {$productPrice} : 결제된 상품의 가격
- {$productQuantity} : 결제된 상품의 갯수
- {$device} : 현재 방문한 페이지의 분류. 아래 4가지 값 중 하나를 가져야한다.
 - PW : PC Web
 - MW : Mobile Web
 - MI : Mobile iOS
 - MA : Mobile Android
- {$orderId} : 결제완료된 주문 ID
- {$orderPrice} : 결제완료된 주문의 가격
- {$userId} : 방문한 유저의 로그인 아이디 (optional) 법적이슈의 문제로 HASH 값을 넣어주는 것이 일반적이다.

