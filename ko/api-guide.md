## Search > Word Suggestion > API 가이드



### 단어 교정 API

#### 요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
| --- | --- |
| POST | [https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/suggest](https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/suggestion) |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[요청 본문]
```
curl -X POST 'https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/suggest' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "word": "우너피스",
}'
```

[필드]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| word | String | 필수 |  | 한국어 10자(20byte), 영어 20자(20byte) 제한<br>공백, 특수문자, 숫자 입력 제한 | 교정이 필요한 단어 |

#### 응답

[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "requestWord": "우너피스"
        "suggestWord": "원피스"
        "isSuggest": true
    }
}
```

[헤더]

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| isSuccessful | Boolean | 단어 교정 API 성공 여부 |
| resultCode | Integer | 결과 코드 |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

[필드]


| 이름 | 타입      | 설명 |
| --- | --- | --- |
| requestWord | String | 요청 단어 |
| suggestWord | String | 교정 결과  |
| isSuggest   | Boolean| 교정 성공 여부  |


### 단어 조회 API

요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
| --- | --- |
| GET | https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[Query]

| 이름 | 타입 | 필수 | 설명                                                                                                    |
| --- | --- | --- |-------------------------------------------------------------------------------------------------------|
| sortKey | String | - | 단어 목록 정렬할 때 사용할 속성<br>`update_datetime`: 최신 업데이트순(기본값)<br>`create_datetime`: 단어 생성순<br>`word`: 단어 이름순 |
| word | String | - | {word} 문자열을 포함하는 단어                                                                                   |
| sortDirection | String | - | 단어 목록 정렬할 속성<br>`asc`: 오름차순<br>`desc`: 내림차순(기본값)                                                      |
| page | Long | - | 페이지                                                                                                   |
| limit | Long | - | 반환할 단어 개수(최대 5,000개)                                                                                  |

[요청 본문]

```
curl -X GET 'https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
```

#### 응답

[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "totalCount": 2
        "dictionary": [
            {
                "word": "원피스",
                "createDatetime": "2023-01-26T15:36:11.000+09:00",
                "updateDatetime": "2023-01-26T15:36:11.000+09:00"
            },
            {
                "word": "이무기",
                "createDatetime": "2023-01-26T15:29:09.000+09:00",
                "updateDatetime": "2023-01-26T15:29:09.000+09:00"
            }
        [
    }
}
```

[헤더]

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| isSuccessful | Boolean | 단어 조회 API 성공 여부 |
| resultCode | Integer | 결과 코드 |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

[필드]

| 이름                        | 타입      | 설명       |
|---------------------------|---------|----------|
| totalCount                | Integer | 단어 전체 개수 |
| dictionary                | Array   | 단어 목록    |
| dictionary.word           | String  | 단어 이름    |
| dictionary.createDatetime | Datetime   | 단어 생성 시각 |
| dictionary.updateDatetime | Datetime   | 단어 수정 시각 |

[실패 응답]

```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4000002,
        "resultMessage": "The service usage setting is disabled"
    }
}
```

### 단어 추가 API

요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
| --- | --- |
| POST | [https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[요청 본문]

```
curl -X POST 'https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "words": [
    "원피스",
    "바닐라라떼"
  ]
}'
```

[필드]

| 이름 | 값 | 필수 여부 |
| --- | --- |-------|
| words | Array | 필수    |

[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[헤더]

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| isSuccessful | Boolean | 단어 추가 API 성공 여부 |
| resultCode | Integer | 결과 코드 |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

### 단어 수정 API

요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
| --- | --- |
| PUT | [https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[요청 본문]

```
curl -X PUT 'https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
```

[필드]

| 이름 | 타입 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| word | String | 필수 | 변경 전 단어 |
| updateWord | String | 필수 |  변경 후 단어 |

[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[헤더]

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| isSuccessful | Boolean | 단어 변경 API 성공 여부 |
| resultCode | Integer | 결과 코드 |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

### 단어 삭제 API

요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
| --- | --- |
| DELETE | [https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[요청 본문]

```
curl -X DELETE'https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "words": [
      "원피스"
      "이무기"
  ]
}
```

[필드]

| 이름    | 타입    | 필수 여부  | 설명       |
|-------|-------| --- |----------|
| words | Array | 필수 | 삭제 단어 목록 |

[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[헤더]

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| isSuccessful | Boolean | 단어 삭제 API 성공 여부 |
| resultCode | Integer | 결과 코드 |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

### 서비스 이용 설정 조회 API

요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
| --- | --- |
| GET | [https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/service-use](https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
    serviceUseStatusCode: "ENABLE"
}
```

[헤더]

| 이름 | 타입 | 설명                               |
| --- | --- |----------------------------------|
| isSuccessful | Boolean | 서비스 이용 설정 조회 API 성공 여부           |
| resultCode | Integer | 결과 코드                            |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

[필드]

| 이름 | 타입 | 설명           |
| --- |-----|--------------|
| serviceUseStatusCode | String | 서비스 이용 상태 코드 |

### 서비스 이용 설정 변경 API

요청

* {appKey}와 {secretKey}는 콘솔 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

[URI]

| 메서드 | URI |
|-----| --- |
| PUT | [https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/{appKey}/service-use](https://word-suggestion.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[요청 헤더]

| 이름 | 값 | 설명              |
| --- | --- |-----------------|
| Authorization | {secretKey} | 콘솔에서 발급 받은 보안 키 |
| Content-Type | application/json |                 |

[필드]

| 이름 | 타입 | 설명                            |
| --- |-----|-------------------------------|
| serviceUseStatusCode | String | 서비스 이용 상태 코드(ENABLE, DISABLE) |


[응답 본문]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[헤더]

| 이름 | 타입 | 설명                            |
| --- | --- |-------------------------------|
| isSuccessful | Boolean | 서비스 이용 설정 변경 API 성공 여부        |
| resultCode | Integer | 결과 코드                         |
| resultMessage | String | 결과 메시지(성공 시 success, 실패 시 오류 내용) |

