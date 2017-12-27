# IIOT Login Module Webhook #

**IIOT 登入模組** 提供第三方開發者 Webhook 功能，當用戶登入**IIOT WiFiOTG平台**時，平台將把使用者登入資訊Webhook給第三方所設置的網址。

## Webhook 格式 ##

- businessId: 企業ID
- activityId: 活動ID
- secret: webhook密碼
- events: 在登入時，event為`login`
- data: 登入用戶資料(依照不同登入方式有所不同)

**會員、SMS登入格式範例**

```json
{
    "businessId": "Mwq5GAxpR",
    "activityId": "yORlxLLMb",
    "secret": "1234",
    "events": "login",
    "data": {
        "lastAuth": 1487039945869,
        "authProvider": "iiot",
        "phoneNumber": "+886921185084"
    },
    "ts": 1487039945961
}
```
**Facebook登入格式範例**

```json
{
    "businessId": "wVwPoqmmw",
    "activityId": "qDX2BLXg4",
    "secret": "abcd", // Securing your web hook
    "events": "login",
    "data": {
        "authProvider": "facebook",
        "id": "1234", // Facebook Id
        "displayName": "Kay Lai",
        "lastAuth": 1451023745099,
        "link": "https://www.facebook.com/app_scoped_user_id/1234/",
        "picture": "https://graph.facebook.com/1234/picture?type=large",
        /* 以下optional */
        "birthday": "MM/DD/YYYY",
        "email": "k@iiot.io",
        "first_name": "Kay",
        "gender": "female",
        "hometown": {
            "id": "109526399066760",
            "name": "Taoyuan District, Taoyuan"
        },
        "locale": "zh_TW",
        "location": {
            "id": "109526399066760",
            "name": "Taoyuan District, Taoyuan"
        },
        "name": "Kay Lai",
        "timezone": 8,
        "updated_time": "2015-10-25T05:47:01+0000",
        "verified": true
    },
    "ts": 1451023745099
}
```

## 設定Webhook ##

於IIOT後台***行銷活動*** 的***登入模組*** 進階設定中，可以設定 ***Webhook*** ，設定值包括：

- 網址：Webhook的目標網址，系統會以`POST`方式將資料送往此目標網址。例如`https://server-example/user`
- 驗證碼：設置目標網址後，IIOT平台需驗證此網址擁有者，因此目標網址須設定(或透過右方***建立驗證碼***來建立)一串驗證碼字串，並讓目標網址的`GET`能回傳此驗證碼字串，供IIOT平台認證使用。
- 密碼：供第三方認證資料來源為IIOT平台

###設定範例###

網址：https://server-example/user
驗證碼：5b9359136f2c6dc353b4fd8c918fdba74ff44433
密碼：test12345

** 流程 **

```sequence

IIOT平台->第三方目標網址: GET
Note right of 第三方目標網址: 根據設定的驗證碼(validator)回傳
第三方目標網址->IIOT平台: 5b9359136f2c6dc353b4fd8c918fdba74ff44433
Note over IIOT平台: 驗證成功

Note over IIOT平台, 第三方目標網址: Webhook
IIOT平台-->第三方目標網址: POST Data with the secret (test12345)
IIOT平台-->第三方目標網址: POST Data with the secret (test12345)
IIOT平台-->第三方目標網址: POST Data with the secret (test12345)
```