# IIOT Email Template Example #

## Parameters ##

參數種類

### 1. formResult ###
表單填寫資訊

- 姓名：`{{formResult.name}}`
- 郵件地址：`{{formResult.email}}`
- 電話：`{{formResult.phoneNumber}}`
- 出發日期：`{{formResult.departureDate}}`
- 出發班機：`{{formResult.departureFlightNo}}`
- 宅配地址: `{{formResult.shipmentAddress}}`
- 回國日期: `{{formResult.arrivalDate}}`
- 回程航班: `{{formResult.arrivalFlightNo}}`
- 還機地點: `{{formulaResult.returnMethod}}`
- 台數：`{{formResult.amount}}`
- 優惠碼: `{{formResult.couponCode}}`

### 2. formulaResult ###
電商運算結果

- 取件地點: `{{formulaResult.pickupMethod}}`
- 總價: `{{formulaResult.total}}`
- 優惠說明: `{{formulaResult.couponDesc}}`
- 優惠折扣:`{{formulaResult.couponDiscountAmount}}`

### 3. invoice ###
帳單明細/付款相關

- 訂單編號: `{{invoice.MerchantOrderNo}}`
- 付款方式: `{{invoice.PaymentType}}`
- 金額: `{{invoice.Amt}}`
- 交易編號: `{{invoice.TradeNo}}`
- 付款時間: `{{invoice.PayTime}}`
- 訂單連結: `{{invoice.url}}`
- 訂單驗證碼: `{{invoice.pin}}`
- 銀行代碼: `{{invoice.BankCode}}`
- 繳費代碼: `{{invoice.CodeNo}}`
- 繳費終止日期: `{{invoice.ExpireDate}}`
- 繳費終止時間: `{{invoice.ExpireTime}}`

## 範例 ##

**訂單通知**

```
Hello {{formResult.name}}
收到你的預訂資料囉，請確認一下您的資訊是否都正確喔

---
姓名：{{formResult.name}}
電話：{{formResult.phoneNumber}}
出發日期：{{formResult.departureDate}}
出發班機：{{formResult.departureFlightNo}}
取件地點: {{formulaResult.pickupMethod}}
宅配地址: {{formResult.shipmentAddress}}
回國日期: {{formResult.arrivalDate}}
回程航班: {{formResult.arrivalFlightNo}}
還機地點: {{formulaResult.returnMethod}}
台數：{{formResult.amount}}
優惠碼: {{formResult.couponCode}}

--
訂單資訊：{{invoice.url}} (驗證碼：{{invoice.pin}})
訂單編號: {{invoice.MerchantOrderNo}}
付款方式: {{invoice.PaymentType}}
金額: {{invoice.Amt}}
交易編號: {{invoice.TradeNo}}
付款時間: {{invoice.PayTime}}

如果有任何問題，歡迎與我們聯繫
祝您有個美好的一天 ^_^

Go WiFi 客服小組 敬上
FB:  https://www.facebook.com/52gowifi
Tel: 02-85222608 (09:00-20:00) 
Email: contact@gowifi.com.tw
Line: https://line.me/ti/p/%40vlx3022p

```

**繳費資訊**
```
Hello {{formResult.name}},

以下是您的繳款資訊 :

訂單資訊：{{invoice.url}}
訂單編號:{{invoice.MerchantOrderNo}}
付款方式:{{invoice.PaymentType}}
金額:{{invoice.Amt}}
交易編號:{{invoice.TradeNo}}

金融機構代碼:{{invoice.BankCode}}
繳費代碼:{{invoice.CodeNo}}
繳費終止日期:{{invoice.ExpireDate}}{{invoice.ExpireTime}}

如果有任何問題，歡迎與我們聯繫
祝您有個美好的一天 ^_^

Go WiFi 客服小組 敬上
FB: https://www.facebook.com/52gowifi
Tel: 02-85222608 (09:00-20:00) 
Email: contact@gowifi.com.tw
```