# 領還機 Webhook 格式說明 #

###領機產品檢核格式範例 ###

領還系統發機前，會呼叫產品檢核Url，依據此Url回傳的資訊，來確認方案與產品可否發機。

**可發機回傳格式**
```
{
    "result": {
        "success": true
    }
}
```
**不可發機回傳格式**
```
{
    "error": {
        "message": "產品與訂單方案不符合"
    }
}
```

**資料格式**

- secret: 根據Admin Portal設定的密碼，在Webhook 傳送資料時，會以`secret`傳送，供第三方程式驗證資料來源是否為**IIOT平台**

- events: 領機的event為`wms-checking`
- data: 傳送的資料內容，領機資料內容包含了：
	- products: 此訂單所綁定的產品，會根據產品種類區分
	- remove: 若此訂單更新後，有產品解除綁定，會被放在remove，供第三方程式同步狀態
	- operator: 處理此取機訂單的人員
	- remark: 領機備註
	- orderNo: 訂單編號
	- counterId: 領機櫃檯id
	- urgent: 是否為急單(1/9)
- ts: 領機時間(ms)

```
 {
     "secret": "12345",
     "events": "wms-checking",
     "data": {
         "products": [{
             "supplier": "GOWIFI",
             "label": "GOWIFI日本",
             "serialNos": ["GOWIFI01", "GOWIFI02"]
         }, {
             "supplier": "KKADD",
             "label": "KKWIFI",
             "serialNos": ["KKADD01"]
         }],
         "remove": [{
             "label": "GOWIFI日本",
             "supplier": "GOWIFI",
             "serialNos": ["OLD1"]
         }, {
             "label": "JETFI",
             "supplier": "JETFI日本",
             "serialNos": ["OLD2"]
         }],
         "operator": "office",
         "remark": "",
         "orderNo": "401478069139087",
         "urgent": 1,
         "counterId": "t2-5"
     },
     "ts": 1484392667488
 }
```

###領機Webhook格式範例 ###

當領機成功，系統會呼叫領機成功Webhook進行通知。

- secret: 根據Admin Portal設定的密碼，在Webhook 傳送資料時，會以`secret`傳送，供第三方程式驗證資料來源是否為**IIOT平台**

- events: 領機的event為`opage-checkin`
- data: 傳送的資料內容，領機資料內容包含了：
	- products: 此訂單所綁定的產品，會根據產品種類區分
	- remove: 若此訂單更新後，有產品解除綁定，會被放在remove，供第三方程式同步狀態
	- operator: 處理此取機訂單的人員
	- remark: 領機備註
	- orderNo: 訂單編號
	- counterId: 領機櫃檯id
	- urgent: 是否為急單(1/9)
- ts: 領機時間(ms)

```
 {
     "secret": "12345",
     "events": "opage-checkin",
     "data": {
         "products": [{
             "supplier": "GOWIFI",
             "label": "GOWIFI日本",
             "serialNos": ["GOWIFI01", "GOWIFI02"]
         }, {
             "supplier": "KKADD",
             "label": "KKWIFI",
             "serialNos": ["KKADD01"]
         }],
         "remove": [{
             "label": "GOWIFI日本",
             "supplier": "GOWIFI",
             "serialNos": ["OLD1"]
         }, {
             "label": "JETFI",
             "supplier": "JETFI日本",
             "serialNos": ["OLD2"]
         }],
         "operator": "office",
         "remark": "",
         "orderNo": "401478069139087",
         "urgent": 1,
         "counterId": "t2-5"
     },
     "ts": 1484392667488
 }
```

###還機Webhook範例###

當設備歸還，系統會呼叫還機Webhook進行通知。

- secret: 根據Admin Portal設定的密碼，在Webhook 傳送資料時，會以`secret`傳送，供第三方程式驗證資料來源是否為**IIOT平台**

- events: 領機的event為`opage-checkout`
- data: 傳送的資料內容，領機資料內容包含了：
	- vendor: 上傳廠商帳戶
	- serialNo: 產品序號
	- supplier: 產品供應商
	- orderNo: 產品關聯訂單號
	- label: 產品名稱
	- operator: 還機處理人員
	- issues: 產品損壞列表
	- remark: 還機備註
	- status: 產品狀態
	- counterId: 還機櫃檯id
- ts: 領機時間(ms)

```
{
    "secret": "test",
    "events": "opage-checkout",
    "data": {
        "vendor": "root@1",
        "serialNo": "TEST123456",
        "supplier": "TESTWIFI",
        "orderNo": "m17011101",
        "label": "TESTWIFI Japan",
        "operator": "gowifi",
        "issues": null,
        "remark": null,
        "status": "RETURN",
        "counterId": "gowifioffice-6"
    },
    "ts": 1484314172919
}
```

## 設定Webhook ##

於IIOT後台***公司設定*** 填寫 ，設定值包括：

- 網址：Webhook的目標網址，系統會以`POST`方式將資料送往此目標網址。例如`https://server-example/user`
- 驗證碼：設置目標網址後，IIOT平台需驗證此網址擁有者，因此目標網址須設定(或透過右方***建立驗證碼***來建立)一串驗證碼字串，並讓目標網址的`GET`能回傳此驗證碼字串，供IIOT平台認證使用。
- 密碼：供第三方認證資料來源為IIOT平台

###設定範例###

網址：https://server-example/user
驗證碼：5b9359136f2c6dc353b4fd8c918fdba74ff44433
密碼：test12345

** 流程 **

![sequence](https://userfiles.iiot.io/businesses/DvxGN8MJp/k83vmzGNY)

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