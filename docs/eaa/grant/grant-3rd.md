# IIOT WiFiOTG 第三方允許上網模組串接流程

## 流程圖

![enter image description here](https://userfiles.iiot.io/businesses/vlzg3B1m8/71R8Y8DYO)

## 流程說明

1. 設備將用戶導向 IIOT Cloud
2. 根據設定，IIOT Cloud將用戶導向第三方認證網頁
3. 認證完成，第三方認證網頁根據 base_grant_url 將用戶導回IIOT

## 參數說明

**步驟2 IIOT Cloud 帶給第三方認證網頁的參數包括:**

1. node_id: 設備的cuid
2. node_mac: 設備的mac address
3. client_mac: 用戶的mac
4. client_ip: 用戶的ip
5. ssid: 用戶透過設備的哪一組ssid連上
6. ts: timestamp
7. base_grant_url: 認證後導向網址

**步驟3 認證後允許上網**

認證通過後要允許用戶上網時，將用戶導回`base_grant_url`，並帶以下參數：

1. ts: timestamp
2. duration: 要允許上網多久 (second)
3. client_mac: 用戶的mac
4. node_mac: 設備的mac
5. ssid: 用戶透過設備的哪一組ssid連上
6. sign: sha1(client_mac + node_mac + ssid + ts + duration + secret)

**base_grant_url 是變動的**

## 範例

用戶導向第三方認證網頁

```http
https://3rdparty.com/auth?base_grant_url=https%3A%2F%2Fwifiotg-dev.iiot.io%2Fmodules%2Fgrant3rd_callback%2Fj61zair4&client_mac=kk%3Akk%3Akk%3A00%3A00%3A12&client_ip=172.18.101.92&node_mac=74%3A19%3Af8%3Ae0%3A35%3A1e&node_id=1e059cc0-6c2a-11e7-8955-1bde0f529b36&ssid=1&ts=1502099585915&activity_id=dBEYmq5X3
```

第三方認證頁面導回IIOT允許上網

```http
https://wifiotg-dev.iiot.io/modules/grant3rd_callback/j61zair4?ts=1502099585915&duration=3600&client_mac=kk:kk:kk:00:00:12&node_mac=74:19:f8:e0:35:1e&ssid=1&sign=f12c5b0b681f2982d7ed3baff6c3ecc355577bc1
```


