## Search > Word Suggestion > API Guide



### Correct Word API

#### Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
| --- | --- |
| POST | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/suggest](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/suggestion) |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Request Body]
```
curl -X POST 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/suggest' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "word": "우너피스",
}'
```

[Field]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| word | String | Required |  | Up to 10 Korean characters (20 byte), 20 English characters (20 byte)<br>Limitation on space, special characters, and numbers | Word that requires correction |

#### Response

[Response Body]

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

[Header]

| Name | Type | Description |
| --- | --- | --- |
| isSuccessful | Boolean | Correct Word API success or not |
| resultCode | Integer | Result code |
| resultMessage | String | Result message (success on success, error content on failure) |

[Field]


| Name | Type      | Description |
| --- | --- | --- |
| requestWord | String | Requested word |
| suggestWord | String | Correction result  |
| isSuggest   | Boolean| Correction success or not  |


### Search Word API

Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
| --- | --- |
| GET | https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Query]

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| sortKey | String | - | Property to use when sorting out words<br>`update_datetime`: Sort by last updated (Default)<br>`create_datetime`: Sort by word created first<br>`word`: Sort by word name |
| word | String | - | {word} words containing strings |
| sortDirection | String | - | Property to sort words<br>`asc`: Ascending order<br>`desc`: Descending order (Default) |
| page | Long | - | Page |
| limit | Long | - | Number of words to return |

[Request Body]

```
curl -X GET 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
```

#### Response

[Response Body]

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

[Header]

| Name | Type | Description |
| --- | --- | --- |
| isSuccessful | Boolean | Search Word API success or not |
| resultCode | Integer | Result code |
| resultMessage | String | Result message (success on success, error content on failure) |

[Field]

| Name | Type | Description           |
| --- | --- |-----------------------|
| totalCount | Integer | Total number of words |
| words | Array | Word list             |
| dictionary                | Array   | Word list             |
| dictionary.word           | String  | Word                  |
| dictionary.createDatetime | Datetime   | Word created time     |
| dictionary.updateDatetime | Datetime   | Word updated time     |

[Failure Response]

```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4000002,
        "resultMessage": "The service usage setting is disabled"
    }
}
```

### Add Word API

Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
| --- | --- |
| POST | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Request Body]

```
curl -X POST 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "words": [
    "원피스",
    "바닐라라떼"
  ]
}'
```

[Field]

| Name | Value | Required |
| --- | --- |-------|
| words | Array | Required    |

[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[Header]

| Name | Type | Description |
| --- | --- | --- |
| isSuccessful | Boolean | Add Word API success or not |
| resultCode | Integer | Result code |
| resultMessage | String | Result message (success on success, error content on failure) |

### Modify Word API

Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
| --- | --- |
| PUT | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Request Body]

```
curl -X PUT 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
```

[Field]

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| word | String | Required | Word before update |
| updateWord | String | Required |  Word after update |

[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[Header]

| Name | Type | Description |
| --- | --- | --- |
| isSuccessful | Boolean | Modify Word API success or not |
| resultCode | Integer | Result code |
| resultMessage | String | Result message (success on success, error content on failure) |

### Delete Word API

Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
| --- | --- |
| DELETE | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Request Body]

```
curl -X DELETE'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "words": [
    "원피스",
    "바닐라라떼"
  ]
}
```

[Field]

| Name | Type   | Required | Description         |
| --- |--------| -- |---------------------|
| words | Array  | Required | Word list to delete |
[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[Header]

| Name | Type | Description |
| --- | --- | --- |
| isSuccessful | Boolean | Delete Word API success or not |
| resultCode | Integer | Result code |
| resultMessage | String | Result message (success on success, error content on failure) |

### Search Service Use Settings API

Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
| --- | --- |
| GET |  [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/service-use](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary)  |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Response Body]

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

[Header]

| Name | Type | Description                               |
| --- | --- |----------------------------------|
| isSuccessful | Boolean | Search Service Use Settings API success or not           |
| resultCode | Integer | Result code                            |
| resultMessage | String | Result message (success on success, error content on failure) |

[Field]

| Name | Type | Description           |
| --- |-----|--------------|
| serviceUseStatusCode | String | Service Use Status Code |

### Change Service Use Settings API

Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
|-----| --- |
| PUT | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/service-use](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary)  |

[Request Header]

| Name | Value | Description |
| --- | --- | --- |
| Authorization | {secretKey} | Security key issued from the console |
| Content-Type | application/json |  |

[Field]

| Name | Type | Description                            |
| --- |-----|-------------------------------|
| serviceUseStatusCode | String | Service use status code (ENABLE, DISABLE) |


[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[Header]

| Name | Type | Description                            |
| --- | --- |-------------------------------|
| isSuccessful | Boolean | Change Service Use Settings API success or not        |
| resultCode | Integer | Result code                         |
| resultMessage | String | Result message (success on success, error content on failure) |

