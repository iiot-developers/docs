# 識別證報到

## Webhook 設定

編輯 活動卡 > 識別證報到，切換到進階選單，可以設定Webhook

設定值包括：

**網址：**

Webhook的目標網址，系統會以`POST`方式將資料送往此目標網址。例如`https://server-example/user`

**驗證碼：**

設置目標網址後，IIOT平台需驗證此網址擁有者，因此目標網址須設定(或透過右方***建立驗證碼***來建立)一串驗證碼字串，並讓目標網址的`GET`能回傳此驗證碼字串，供IIOT平台認證使用。

**密碼：**

供第三方認證資料來源為IIOT平台

### 設定範例

網址：https://server-example/user
驗證碼：5b9359136f2c6dc353b4fd8c918fdba74ff44433
密碼：test12345

** 流程 **

![sequence](https://userfiles.iiot.io/businesses/DvxGN8MJp/k83vmzGNY)

### Ｗebhook Data 範例

```
{
    "secret": "aaaa",
    "events": "checkin",
    "data": {
        "barcodeMessage": "E775500003691",
        "changeBarcodeOn": false
    },
    "ts": 1513848889294
}
```