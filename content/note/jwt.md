---
title: "Jwt"
date: 2022-09-20T09:16:39+08:00
draft: false
keywords: Jwt
description: ""
weight: 1
---

# JWT 
json 開放標準 [rfc7519](https://www.rfc-editor.org/rfc/rfc7519)，全名為 JSON Web Token， 是數位簽章(Digital Signature)的其中一種，用於兩個網絡服務器之間的資料傳送，如 app 的使用者端與伺服器端。
JWT 的加密演算法有HMAC、RSA、ECDS，而是實際可以使用 密碼(經過 HMAC 演算法) 或用一對 公鑰/私鑰(經過 RSA 或 ECDSA 演算法) 來對 JWT 進行簽章。

# 結構
1.  header
2.  payload
3.  signature/encryption data
> 其中前兩個元素 header 和 payload 是特定結構的 JSON 物件，第三個部分取決於演算法是用來作簽章還是加密，如果是未加密的 JWT，則將其省略。JWT 可以被編碼成 JWS/JWE 簡潔的表現形式(Compact Serialization)。JWS 和 JWE 規範中定義了另一種序列化格式，稱為 JSON 序列化，這是一種非簡潔的表示形式，允許在同一 JWT 中使用多個簽章或接收者。

> 簡潔的序列化(The compact serialization)是對前兩個 UTF-8 字節的 JSON 元素（header 和 payload）以及進行簽章或加密的 data(不是 JSON 物件本身) 做 Base64 URL 安全編碼。三部分分別用一個 . 隔開。
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.  # header
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.  # payload
TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ  # signature
```

# 使用時機
* 授權： 
  這是使用 JWT 最常見的場景。JWT 用於授權而非身份驗證。通過身份驗證，我們驗證用戶名和密碼是否有效，並將用戶登錄到系統中。通過授權，我們可以驗證發送到服務器的請求是否屬於通過身份驗證登錄的用戶，從而可以授予該用戶訪問系統的權限，繼而批准該用戶使用獲得的 token 訪問路由、服務和資源。

* 信息交換： 
  JSON Web Token 是在雙方之間安全地傳輸信息的一種好方法。因爲 JWT 可以被簽名（例如，使用公鑰 / 私鑰對），所以使您能確保發送方是他們所聲稱的那一方。此外，由於簽名是使用 Header 和 Payload 計算的，能驗證發送的內容沒有被篡改。


# 參考：
[what-is-jwt](https://5xruby.tw/posts/what-is-jwt)
[企鵝也懂程式設計](https://medium.com/%E4%BC%81%E9%B5%9D%E4%B9%9F%E6%87%82%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88/jwt-json-web-token-%E5%8E%9F%E7%90%86%E4%BB%8B%E7%B4%B9-74abfafad7ba)
[JSON Web Token (JWT) 简介](https://mozillazg.com/2015/06/hello-jwt.html)