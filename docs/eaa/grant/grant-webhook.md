# IIOT WiFi Grant Webhook #

**設定方式**

於**IIOT Admin**後台編輯***行銷活動***，點開***進階模式***設定***用戶允許上網Webhook***

將會於用戶被允許上網時，收到如下的資料格式：

- businessId: 您的企業ID
- secret: 您設定的webhook密碼
- events: 此事件為`wifi-grant`
- data: Webhook所帶的資料，包括`network`,`visitor`,`activity`,`business`
	- network: 提供`iNodeId`(允許用戶上線的設備ID)以及`clientMac`(用戶設備的MAC Address)
	- visitor: 用戶登入的帳戶資訊
	- activity: 活動ID與名稱
	- business: 企業ID與名稱

```
{
    "businessId": "YOUR_BUSINESSID",
    "secret": "YOUR_SETTING_SECRET",
    "events": "wifi-grant",
    "data": {
        "network": {
            "iNodeId": "INODE_CUID_STRING",
            "clientMac": "aa:bb:cc:dd:ee:ff"
        },
        "visitor": {
            "vuid": "VISITOR_ID",
            "lastAuth": 1489595011572,
            "phoneNumber": "+886900000000",
            "authProvider": "iiot"
        },
        "activity": {
            "id": "ACTIVITY_ID",
            "name": "My Activity"
        },
        "business": {
            "id": "BUSINESS_ID",
            "name": "My Business Name"
        }
    },
    "ts": 1489595012146
}
```