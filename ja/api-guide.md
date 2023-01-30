## Search > Word Suggestion > APIガイド



### 単語校正API

#### リクエスト

* {appKey}と{secretKey}は、コンソール上部の**URL & Appkey** メニューで確認できます。

[URI]

| メソッド | URI |
| --- | --- |
| POST | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/suggest](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/suggestion) |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[リクエスト本文]
```
curl -X POST 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/suggest' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "word": "ウナピース",
}'
```

[フィールド]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| word | String | 必須 |  | 韓国語10文字(20byte)、英語20文字(20byte)制限<br>空白、特殊文字、数字入力制限 | 校正が必要な単語 |

#### レスポンス

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "requestWord": "ウナピース"
        "suggestWord": "ワンピース"
        "isSuggest": true
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| isSuccessful | Boolean | 単語校正API成否 |
| resultCode | Integer | 結果コード |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]


| 名前 | タイプ  | 説明 |
| --- | --- | --- |
| requestWord | String | リクエスト単語 |
| suggestWord | String | 校正結果 |
| isSuggest   | Boolean| 校正成否 |


### 単語照会API

リクエスト

* {appKey}と{secretKey}はコンソール上部の**URL & Appkey**メニューで確認できます。

[URI]

| メソッド | URI |
| --- | --- |
| GET | https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[Query]

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| sortKey | String | - | 単語リストをソートする時に使用するプロパティ<br>`update_datetime`：最新アップデート順(デフォルト値)<br>`create_datetime`：単語作成順<br>`word`：単語名順 |
| word | String | - | {word}文字列を含む単語 |
| sortDirection | String | - | 単語リストをソートするプロパティ<br>`asc`：昇順<br>`desc`：降順(デフォルト値) |
| page | Long | - | ページ |
| limit | Long | - | 返す単語数 |

[リクエスト本文]

```
curl -X GET 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
```

#### レスポンス

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "totalCount": 2
        "words": [
            "ワンピース"
            "大蛇"
        [
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| isSuccessful | Boolean | 単語照会API成否 |
| resultCode | Integer | 結果コード |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| totalCount | Integer | 単語全体数 |
| words | Array | 単語リスト |

[失敗レスポンス]
* Content-Type: application/json

```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4000002,
        "resultMessage": "The service usage setting is disabled"
    }
}
```

### 単語追加API

リクエスト

* {appKey}と{secretKey}はコンソール上部の **URL & Appkey** メニューで確認できます。

[URI]

| メソッド | URI |
| --- | --- |
| POST | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[リクエスト本文]

```
curl -X POST 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "words": [
    "ワンピース",
    "バニララテ"
  ]
}'
```

[フィールド]

| 名前 | 値 | 必須かどうか |
| --- | --- |-------|
| words | Array | 必須 |

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| isSuccessful | Boolean | 単語追加API成否 |
| resultCode | Integer | 結果コード |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

### 単語修正API

リクエスト

* {appKey}と{secretKey}はコンソール上部の **URL & Appkey** メニューで確認できます。

[URI]

| メソッド | URI |
| --- | --- |
| PUT | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[リクエスト本文]

```
curl -X PUT 'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
```

[フィールド]

| 名前 | タイプ | 必須かどうか | 説明 |
| --- | --- | --- | --- |
| word | String | 必須 | 変更前単語 |
| updateWord | String | 必須 | 変更後単語 |

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| isSuccessful | Boolean | 単語変更API成否 |
| resultCode | Integer | 結果コード |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

### 単語削除API

リクエスト

* {appKey}と{secretKey}はコンソール上部の **URL & Appkey** メニューで確認できます。

[URI]

| メソッド | URI |
| --- | --- |
| DELETE | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[リクエスト本文]

```
curl -X DELETE'https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/words'
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "word": "トマトスパゲティ"
}
```

[フィールド]

| 名前 | タイプ | 必須かどうか | 説明 |
| --- | --- | --- | --- |
| word | String | 必須 | 削除単語 |

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| isSuccessful | Boolean | 単語削除API成否 |
| resultCode | Integer | 結果コード |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

### サービス利用設定照会API

リクエスト

* {appKey}と{secretKey}はコンソール上部の **URL & Appkey** メニューで確認できます。

[URI]

| メソッド | URI |
| --- | --- |
| GET | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/service-use](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[レスポンス本文]

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

[ヘッダ]

| 名前 | タイプ | 説明                           |
| --- | --- |----------------------------------|
| isSuccessful | Boolean | サービス利用設定照会API成否       |
| resultCode | Integer | 結果コード                        |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]

| 名前 | タイプ | 説明       |
| --- |-----|--------------|
| serviceUseStatusCode | String | サービス利用ステータスコード |

### サービス利用設定変更API

リクエスト

* {appKey}と{secretKey}はコンソール上部の **URL & Appkey** メニューで確認できます。

[URI]

| メソッド | URI |
|-----| --- |
| PUT | [https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/{appKey}/service-use](https://word-suggestion-alpha.api.nhncloudservice.com/v1.0/appkeys/%7BappKey%7D/word-suggestion/dictionary) |

[リクエストヘッダ]

| 名前 | 値 | 説明          |
| --- | --- |-----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |
| Content-Type | application/json |                 |

[フィールド]

| 名前 | タイプ | 説明                        |
| --- |-----|-------------------------------|
| serviceUseStatusCode | String | サービス利用ステータスコード(ENABLE, DISABLE) |


[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明                        |
| --- | --- |-------------------------------|
| isSuccessful | Boolean | サービス利用設定変更API成否    |
| resultCode | Integer | 結果コード                     |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |
