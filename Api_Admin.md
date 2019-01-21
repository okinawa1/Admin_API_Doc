# 支付中心 Admin API

## 规范说明:

- 编码：`UTF-8`
- Content-Type： `application/json`
- 身分验证： 每次登入后，进行cookie验证模式，并将基本资讯存在 HttpContext
  
- Http响应代码：
```
200： 请求处理成功
400： 参数错误
404： 请求资源（uri）不存在
405： 请求资源（uri）存在，但不支援目前的http-method
500： 伺服器内部错误（通知支付中心技术人员）
```

---

## [索引](#索引)

[1.帐户相关](#1帐户相关)

[2.商户相关](#2商户相关)

[3.交易相关](#3交易相关)

[4.系統管理相关](#4系統管理相关)

[5.系統功能相关](#5系統功能相关)

---


### 1.帐户相关

#### `重点内容`

[1.1.登入](#11登入)

[1.2.登出](#12登出) 

[1.3.修改密码](#13修改密码)

---


#### 1.1.登入

- HttpMethod: `POST` 
- URI: `/api/admin/account/login`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:----------:|:---:|:--:|:--------------------------:|:------------:|
| `username` | 帐号 | N  | 由 Admin 提供的唯一标识号 | admin12345 |
| `password` | 密码 | Y | 登入 Admin 平台的密码 | qaz123 |
| `vcode` | 验证码 | Y | 扫 google 第三方验证码（未确定方案） | 856543 |

</div>

>> [帐户相关](#1帐户相关) | [索引](#索引)

---


#### 1.2.登出

- HttpMethod: `DELETE`
- URI: `/api/admin/account/login`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:----------:|:---:|:--:|:--------------------------:|:------------:|
| `username` | 帐号 | N  | 由 Admin 提供的唯一标识号 | admin12345 |

</div>

>> [帐户相关](#1帐户相关) | [索引](#索引)

---


#### 1.3.修改密码

- HttpMethod: `PATCH`
- URI: `/api/admin/account/password`
    
### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-------------:|:------:|:----:|:--------:|:-------:|
| `username` | 帐号 | N | 由 Admin 提供的唯一标识号 | admin12345 |
| `oldPassword` | 旧密码 | Y | 旧密码 | password123 |
| `newPassword` | 新密码 | Y | 新密码 | 321password |

</div>

>> [帐户相关](#1帐户相关) | [索引](#索引)

---

### 2.商户相关

#### `重点内容`

[2.1.取得商户列表](#21取得商户列表)

[2.2.新增商户资料](#22新增商户资料)

[2.3.取得商户资料](#23取得商户资料)

[2.4.修改商户资料](#24修改商户资料)

[2.5.修改商户状态](#25修改商户状态)

----

#### 2.1.取得商户列表

- HttpMethod: `GET`
- URI: `/api/admin/merchant/merchant`
- API 将会取得所有的商户

### Request 

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `userName` | 商户名称 |  | 商户名称 | 小商户 |
| `status` | 商户状态 |  | 商户状态 | 0 : 关闭, 1 : 启用 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `id` | 商户流水号 | Y | 商户流水号 | 1 |
| `userName` | 商户名称 | Y | 商户的名称 | RB001 |
| `name` | 商户名称 | Y | 商户的简称 | 小小商户 |
| `merchantKey` | 商户金钥 | Y | 商户的特殊金钥 | 77499981 |
| `notes` | 备注 | Y | 备注 | 危险商户 |
| `status` | 商户状态 | Y | 商户状态 | 0 : 关闭, 1 : 启用 |
| `createdAt` | 建立时间 | Y | 建立时间 | yyyy/MM/dd HH:mm:ss |
| `createdByUserName` | 建立者 userName | Y | 建立者 Id | jb12345 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

 </div>
 
>> [商户相关](#2商户相关) | [索引](#索引)

---

#### 2.2.新增商户列表

- HttpMethod: `POST`
- URI: `/api/admin/merchant/merchant`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `userName` | 商户名称 | Y | 商户的名称 | RB001 |
| `name` | 商户名称| Y | 商户的简称 | 小小商户 |
| `merchantKey` | 商户金钥 | Y | 商户的特殊金钥 | 77499981 |
| `notes` | 备注 |  | 备注 | Y |

</div>

>> [商户相关](#2商户相关) | [索引](#索引)

---

#### 2.3.取得商户资料

- HttpMethod: `GET`
- URI: `/api/admin/merchant/merchant`
- API 将会依照 merchantId (商户流水号) 取得该商户所有资讯

### Request 

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `id` | 商户流水号 | Y | 商户流水号 | 1 |

</div>

### Response 

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `id` | 商户流水号 | Y | 商户流水号 | 1 |
| `userName` | 商户名称 | Y | 商户的名称 | RB001 |
| `name` | 商户名称| Y | 商户的简称 | 小小商户 |
| `merchantKey` | 商户金钥 | Y | 商户的特殊金钥 | 77499981 |
| `notes` | 备注 |  | 备注 | Y |
| `status` | 商户状态 | Y | 商户状态 | 0 : 关闭, 1 : 启用 |
| `createdAt` | 建立时间 | Y | 建立时间 | yyyy/MM/dd HH:mm:ss |
| `createdByUserName` | 建立者 userName | Y | 建立者 Id | jb12345 |

</div>

>> [商户相关](#2商户相关) | [索引](#索引)

---

#### 2.4.修改商户资料

- HttpMethod: `PUT`
- URI: `/api/admin/merchant/merchant`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `id` | 商户流水号 | Y | 商户流水号 | 1 |
| `name` | 商户名称| Y | 商户的简称 | 小小商户 |
| `merchantKey` | 商户金钥 | Y | 商户的特殊金钥 | 77499981 |
| `notes` | 备注 |  | 备注 | Y |

</div>

>> [商户相关](#2商户相关) | [索引](#索引)

---

#### 2.5.修改商户状态

- HttpMethod: `PATCH`
- URI: `/api/admin/merchant/merchant`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:-----------:|:--------------:|:---:|:------:|:-------:|
| `id` | 商户流水号 | Y | 商户流水号 | 1 |
| `status` | 商户状态 | Y | 商户状态 | 0 : 关闭, 1 : 启用 |

</div>

>> [商户相关](#2商户相关) | [索引](#索引)

---



### 3.交易相关 

#### `重点内容`

[3.1.支付宝存款列表查询](#31支付宝存款列表查询)

[3.2.支付宝单笔存款详细](#32支付宝单笔存款详细)

[3.3.支付宝单笔存款查询订单](#33支付宝单笔存款查询订单)

[3.4.支付宝单笔存款补发商户回调](#34支付宝单笔存款补发商户回调)

[3.5.在线存款列表查询](#35在线存款列表查询)

[3.6.在线单笔存款详细](#36在线单笔存款详细)

[3.7.在线单笔存款查询订单](#37在线单笔存款查询订单)

[3.8.在线单笔存款补发商户回调](#38在线单笔存款补发商户回调)

[3.9.微信存款列表查询](#39微信存款列表查询)

[3.10.微信单笔存款详细](#310微信单笔存款详细)

[3.11.微信单笔存款查询订单](#311微信单笔存款查询订单)

[3.12.微信单笔存款补发商户回调](#312微信单笔存款补发商户回调)

[3.13.网银存款列表查询](#313网银存款列表查询)

[3.14.网银单笔存款详细](#314网银单笔存款详细)

[3.15.网银单笔存款查询订单](#315网银单笔存款查询订单)

[3.16.网银单笔存款补发商户回调](#316网银单笔存款补发商户回调)

[3.17.充值卡存款列表查询](#317充值卡存款列表查询)

[3.18.充值卡单笔存款详细](#318充值卡单笔存款详细)

[3.19.充值卡单笔存款查询订单](#319充值卡单笔存款查询订单)

[3.20.充值卡单笔存款补发商户回调](#320充值卡单笔存款补发商户回调)

[3.21.QQ钱包存款列表查询](#321QQ钱包存款列表查询)

[3.22.QQ钱包单笔存款详细](#322QQ钱包单笔存款详细)

[3.23.QQ钱包单笔存款查询订单](#323QQ钱包单笔存款查询订单)

[3.24.QQ钱包单笔存款补发商户回调](#324QQ钱包单笔存款补发商户回调)

[3.25.银联支付存款列表查询](#325银联支付存款列表查询)

[3.26.银联支付单笔存款详细](#326银联支付单笔存款详细)

[3.27.银联支付单笔存款查询订单](#327银联支付单笔存款查询订单)

[3.28.银联支付单笔存款补发商户回调](#328银联支付单笔存款补发商户回调)

[3.29.支付宝转卡存款列表查询](#329支付宝转卡存款列表查询)

[3.30.支付宝转卡单笔存款详细](#330支付宝转卡单笔存款详细)

[3.31.支付宝转卡单笔存款查询订单](#331支付宝转卡单笔存款查询订单)

[3.32.支付宝转卡单笔存款补发商户回调](#332支付宝转卡单笔存款补发商户回调)

[3.33.京东钱包存款列表查询](#333京东钱包存款列表查询)

[3.34.京东钱包单笔存款详细](#334京东钱包单笔存款详细)

[3.35.京东钱包单笔存款查询订单](#335京东钱包单笔存款查询订单)

[3.36.京东钱包单笔存款补发商户回调](#336京东钱包单笔存款补发商户回调)

[3.37.灌钱存款列表查询](#337灌钱存款列表查询)

[3.38.灌钱单笔存款详细](#338灌钱单笔存款详细)

[3.39.灌钱单笔存款查询订单](#339灌钱单笔存款查询订单)

[3.40.灌钱单笔存款新增](#340灌钱单笔存款新增)

[3.41.灌钱单笔存款补单](#341灌钱单笔存款补单)

[3.42.提款列表查询](#342提款列表查询)

[3.43.提款资料详细](#343提款资料详细)

[3.44.单笔提款查询订单](#344单单笔提款查询订单)

[3.45.单笔提款补发商户回调](#344单笔提款补发商户回调)

---

#### 3.1.支付宝存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/alipay`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=2 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.2.支付宝单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/alipay`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.3.支付宝单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 2 | 2 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.4.支付宝单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 2 | 2 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.5.在线存款列表查询 (不实作）

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/onlinepayment`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=3 | 1 |
| `depositStatus` | 订单状态 |  | 订单状态下拉选单 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.6.在线单笔存款详细 (不实作）

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/onlinepayment`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 申请金额 | Y | 申请金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.7.在线单笔存款查询订单 (不实作）

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 3 | 3 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.8.在线单笔存款补发商户回调 (不实作）

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 3 | 3 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.9.微信存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/wechat`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=1 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.10.微信单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/wechat`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.11.微信单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 1 | 1 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.12.微信单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 1 | 1 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.13.网银存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/onlinebanking`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `bankName` | 存款银行 | Y | 存款银行 | 招商银行 |
| `payerName` | 收款人 | Y | 收款人 | 收款人一号 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 123456789 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.14.网银单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/onlinebanking`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `bankName` | 存款银行 | Y | 存款银行 | 交通银行 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 申请金额 | Y | 申请金额 | 100.00 |
| `actualAmount` | 到帐金额 |  | 到帐金额 | 100.00 |
| `payerName` | 存款人 | Y | 存款人 | 存款人一号 |
| `payeeName` | 收款人 | Y | 收款人 | 收款人一号 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.15.网银单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 4 | 4 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.16.网银单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 4 | 4 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.17.充值卡存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/prepaidCard`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=5 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.18.充值卡单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/prepaidCard`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.19.充值卡单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 5 | 5 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.20.充值卡单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 5 | 5 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.21.QQ钱包存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/qqwallet`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=6 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.22.QQ钱包单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/qqwallet`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.23.QQ钱包单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 6 | 6 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.24.QQ钱包单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 6 | 6 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.25.银联支付存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/quickpay`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=7 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.26.银联支付单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/quickpay`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.27.银联支付单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 7 | 7 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.28.银联支付单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 7 | 7 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.29.支付宝转卡存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/onlinetobankcard`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `payerName` | 存款人姓名 | Y | 对存款人姓名做模糊查询 | 存款人一号 |
| `payeeName` | 收款人姓名 | Y | 对收款人姓名做模糊查询 | 收款人一号 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=8 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `payerName` | 存款人 | Y | 存款人 | 存款人一号 |
| `payeeName` | 收款人 | Y | 收款人 | 收款人一号 |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.30.支付宝转卡单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/onlinetobankcard`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 申请金额 | Y | 申请金额 | 100.00 |
| `actualAmount` | 到帐金额 |  | 到帐金额 | 100.00 |
| `payerName` | 存款人 | Y | 存款人 | 存款人一号 |
| `payeeName` | 收款人 | Y | 收款人 | 收款人一号 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.31.支付宝转卡单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 8 | 8 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.32.支付宝转卡单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 8 | 8 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.33.京东钱包存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/jdwallet`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=9 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.34.京东钱包单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/jdwallet`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.35.京东钱包单笔存款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 9 | 9 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.36.京东钱包单笔存款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 9 | 9 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.37.灌钱存款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/internal`
- API 将依搜寻条件搜寻出订单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |   | 依商户流水号查询（下拉选单） | 1 |
| `customerUserName` | 帐号 |   | 该商户内使用者的帐号模糊查询 | alan0123 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 |  | 支付中心支付订单号码模糊查询 | CK1809121400588992 |
| `merchantOrderNumber` | 商户订单号 |   | 商户订单号模糊查询 | 18457875884 |
| `depositStatus` | 订单状态 |  | 参考订单状态下拉选单 | 1 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=101 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `isEnableQuery` | 是否查询订单 |  | 如果值为true, 则该列提供"查询订单"功能 | true |
| `isEnableManual` | 是否补发商户回调 |  | 如果值为true, 则该列提供"补发商户回调"功能 | false |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.38.灌钱单笔存款详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/internal`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `depositIP` | 存款IP |  | 存款IP | 127.0.0.1 |
| `requestedAmount` | 存款金额 | Y | 存款金额 | 100.00 |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `depositStatus` | 订单状态 | Y | 订单状态下拉选单的值 | 101 |
| `commission` | 手续费 |  | 手续费 | 100.00 |
| `depositAddress` | 存款地址 |  | 存款地址 | xxxxx |
| `createAt` | 订单建立时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `completedAt` | 完成时间 | Y | 该订单在支付商回调的时间 | yyyy/MM/dd HH:mm:ss |
| `merchantOrderNumber` | 商户订单号 | Y | 商户订单号 | 18457875884 |
| `systemOrderNumber` | 支付中心系统订单号 |  | 支付中心系统订单号 | 18457875884 |
| `paymentCenterOrderNumber` | 支付中心支付订单号 | Y | 支付中心支付订单号 | CK1809121400588992 |
| `paymentOrderNumber` | 支付平台订单号 | Y | 支付平台订单号 | 1236547899 |
| `manualApprovedAt` | 补单时间 |  | 补单时间 | yyyy/MM/dd HH:mm:ss |
| `manualApprovedBy` | 补单人员 |  | 补单人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.39.灌钱单笔存款查询订单

- HttpMethod: `POST`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `paymentMethod` | 支付方式 | Y | 固定值给 101 | 101 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.40.灌钱单笔存款新增

- HttpMethod: `POST`
- URI: `/api/admin/trade/deposit/internal`
- API 新增一笔灌钱订单
- 商户号（下拉单）：参考 取得商户选单

- 先选择商户号后, 才会生成下列选单
- 灌钱银行卡（下拉单）：参考 取得灌钱银行卡选单
- 灌钱银行（下拉单）：参考 取得银行选单 
- 灌钱通道（下拉单）：参考 取得灌钱通道选单

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `depositPaymentChannelId` | 灌钱银行卡 | Y | 依灌钱银行卡下拉单取得 | 146 |
| `bankId` | 灌钱银行 | Y | 依银行总表下拉单取得 | 2 |
| `amount` | 金额 | Y | 灌钱金额 | 100 |
| `paymentChannelId` | 灌钱通道 | Y | 依灌钱通道下拉单取得 | 145 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.41.灌钱单笔存款补单

- Feature: isEnableManualConfirm  (true 才开放此功能)
- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manualconfirm`
- API 将订单列为失败

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `notes` | 补单原因 |  | 补单原因 | 失败 |
| `paymentMethod` | 支付方式 | Y | 从订单列表的栏位取得 | 1 |
| `PaymentType` | 支付类别 | Y | 从订单列表的栏位取得 | 2 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.41.灌钱单笔存款提醒

- Feature: isEnableReminder  (true 才开放此功能)
- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/reminder`
- API 将订单列为等待审核催到账
- 跳出视窗, 列出"商户订单号"和"金额", 无法编辑, 只能送出

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单id | Y | 订单唯一流水号 | 1 |
| `amount` | 金额 | Y | 金额 | 100 |
| `paymentMethod` | 支付方式 | Y | 从订单列表的栏位取得 | 1 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.42.提款列表查询

- HttpMethod: `GET`
- URI: `/api/admin/trade/withdrawal/merchantwithdrawal`
- API 将依搜寻条件搜寻出提款

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户流水号 |  | 依商户流水号查询（下拉选单） | 1 |
| `payeeUserName` | 提款帐号 |  | 该商户内使用者的帐号模糊查询 | alan0123 |
| `payeeName` | 提款姓名 |  | 该商户内使用者的姓名模糊查询 | 陈艾伦 |
| `payeeCardNumber` | 提款卡号 |  | 该商户内使用者的卡号模糊查询 | 6214851251402355 |
| `paymentChannel` | 支付渠道 |  | 支付渠道下拉选单, id=2 | 1 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号模糊查询 | 18457875884 |
| `providerBank` | 提款银行 |  | 参考银行下拉选单 | 1 |
| `withdrawalStatus` | 提款订单状态 |  | 参考提款订单状态下拉选单 | 1 |
| `createAtStart` | 订单建立时间起 |  | 订单在支付商建立的时间起 | yyyy/MM/dd |
| `createAtEnd` | 订单建立时间迄 |  | 订单在支付商建立的时间迄 | yyyy/MM/dd |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `merchantOrderNumber` | 商户订单号 |  | 商户订单号 | 18457875884 |
| `payeeName` | 提款姓名 | Y | 提款姓名 | 王炎 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `commission` | 手续费 | Y | 手续费金额 | 100.00 |
| `bankName` | 提款银行 | Y | 提款银行名称 | 中国工商银行 |
| `payeeCardNumber` | 提款卡号 | Y | 提款卡号 | 6214830220550213 |
| `createdAt` | 申请时间 | Y | 订单在商户建立的时间 | yyyy/MM/dd HH:mm:ss |
| `auditedAt` | 支付时间 | Y | 支付时间 | yyyy/MM/dd HH:mm:ss |
| `paymentChannelName` | 支付渠道名称 | Y | 支付渠道名称 | 快快 微信H5 |
| `withdrawalStatus` | 提款订单状态 | Y | 提款订单状态下拉选单的值 | 101 |
| `merchantCallbackStatus` | 通知状态 | Y | 值若为"通知中"则显示灰色,"通知成功" 则使用绿色 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.43.提款资料详细

- HttpMethod: `GET`
- URI: `/api/admin/trade/withdrawal/merchantwithdrawal`
- API 将依订单流水号捞出该订单详细资料

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 提款订单流水号 | Y | 提款订单流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |
| `merchantName` | 商户帐号 | Y | 商户的帐号 | rb_01 |
| `customerUserName` | 帐号 | Y | 该商户内使用者的帐号 | alan0123 |
| `payeeName` | 提款姓名 | Y | 提款姓名 | 王炎 |
| `requestedAmount` | 金额 | Y | 订单金额 | 100.00 |
| `commission` | 手续费 | Y | 手续费金额 | 100.00 |
| `withdrawalStatus` | 提款状态 |  | 参考提款状态下拉选单 | 1 |
| `payeeCardNumber` | 提款卡号 | Y | 提款卡号 | 6214830220550213 |
| `bankName` | 提款银行 | Y | 提款银行名称 | 中国工商银行 |
| `withdrawalIP` | 提款IP |  | 提款IP | 127.0.0.1 |
| `withdrawalAddress` | 开户地址 | Y | 开户地址 | 北京市 |
| `auditedAt` | 审核时间 |  | 审核时间 | yyyy/MM/dd HH:mm:ss |
| `auditedById` | 审核人员 |  | 审核人员 | Joe |
| `paidAt` | 支付时间 |  | 支付时间 | yyyy/MM/dd HH:mm:ss |
| `paidById` | 支付时间 |  | 支付人员 | Joe |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.44.单笔提款查询订单

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/query`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |

</div>

### Response

纯文字,从Result取得并做弹跳视窗即可

>> [交易相关](#3交易相关) | [索引](#索引)

---

#### 3.45.单笔提款补发商户回调

- HttpMethod: `GET`
- URI: `/api/admin/trade/deposit/feature/manual`
- API 将重新推送该笔订单至支付商查询

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 订单流水号 | Y | 流水号 | 77499981 |

</div>

>> [交易相关](#3交易相关) | [索引](#索引)

---

### 4.系統管理相关 

#### `重点内容`

[4.1.取得角色列表](#41取得角色列表)

[4.2.新增角色](#42新增角色)

[4.3.取得角色资料](#43取得角色资料)

[4.4.修改角色](#44修改角色)

[4.5.角色停用/启用](#45角色停用/启用)

[4.6.取得使用者列表](#46取得使用者列表)

[4.7.新增使用者](#47新增使用者)

[4.8.取得使用者资料](#48取得使用者资料)

[4.9.修改使用者](#49修改使用者)

[4.10.使用者停用/启用](#410使用者停用/启用)

[4.11.支付渠道列表](#411支付渠道列表)

[4.12.新增支付渠道](#412新增支付渠道)

[4.13.修改支付渠道](#413修改支付渠道)

[4.14.支付渠道详情](#414支付渠道详情)

[4.15.支付渠道停用/启用/作废](#415支付渠道停用/启用/作废)

[4.16.取得支付渠道成功率](#416取得支付渠道成功率)

[4.17.银行总表列表](#417银行总表列表)

[4.18.新增银行总表](#418新增银行总表)

[4.19.取得银行总表详细](#419取得银行总表详细)

[4.20.修改银行总表](#420修改银行总表)

[4.21.支付服务商列表](#421支付服务商列表)

[4.22.新增支付服务商](#422新增支付服务商)

[4.23.取得支付服务商详细](#423取得支付服务商详细)

[4.24.修改支付服务商](#424修改支付服务商)

[4.25.支付服务商停用/启用](#425支付服务商停用/启用)

[4.26.支付银行列表](#426支付银行列表)

[4.27.新增支付银行](#427新增支付银行)

[4.28.取得支付银行详细](#428取得支付银行详细)

[4.29.修改支付银行](#429修改支付银行)

[4.30.支付银行停用/启用](#430支付银行停用/启用)

[4.31.业务日志](#431业务日志)

[4.32.业务日志详情](#432业务日志详情)

---

#### 4.1.取得角色列表

- HttpMethod: `GET`
- URI: `/api/admin/system/role`
- API 将依条件取得所有的角色

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `roleName` | 角色名称 |  | 角色名称 | 客服主管 |
| `status` | 状态 |  | 状态 | 启用：1, 禁用：2, 作废：99 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 角色流水号 | Y | 流水号 | 1 |
| `roleName` | 角色名称 | Y | 角色名称 | 客服主管 |
| `createdAt` | 建立时间 | Y | 建立时间 | yyyy/MM/dd HH:mm:ss |
| `createdByUserName` | 建立者 userName | Y | 建立者 Id | jb12345 |
| `status` | 状态 | Y | 状态 | 启用：1, 禁用：2, 作废：99 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.2.新增角色

- HttpMethod: `POST`
- URI: `/api/admin/system/role`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `roleName` | 角色名称 | Y | 角色名称 | 客服主管 |
| `permissionIds` | 权限流水号 id | Y | 该角色可使用的权限的流水号（多笔） | [1, 2, 5, 10]|

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---
#### 4.3.取得角色资料

- HttpMethod: `GET`
- URI: `/api/admin/system/role`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 角色流水号 | Y | 流水号 | 1 

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 角色流水号 | Y | 流水号 | 1 |
| `roleName` | 角色名称 | Y | 角色名称 | 客服主管 |
| `createdById` | 建立人Id | Y | 建立角色的人的 userId | jay1221 |
| `createdAt` | 建立时间 | Y | 角色被建立的时间 | yyyy/MM/dd HH:mm:ss |
| `permissionIds` | 权限流水号 id | Y | 该角色可使用的权限的流水号（多笔） | {1, 2, 5, 10}|
| `status` | 状态 | Y | 状态 | 启用：1, 禁用：2, 作废：99 |
| `subPermissions` | 权限 |  | 树状结构列出 | [ {"id":"1", "name":"name1"}, {"id":"2", "name":"name2"} ] |

</div>
>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.4.修改角色

- HttpMethod: `PUT`
- URI: `/api/admin/system/role`
- 修改角色名称以及权限

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 角色流水号 | Y | 流水号 | 1 |
| `roleName` | 角色名称 | Y | 角色名称 | 客服主管 |
| `permissionIds` | 权限流水号 id | Y | 该角色可使用的权限的流水号（多笔） | {1, 2, 5, 10}|

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.5.角色停用/启用

- HttpMethod: `PATCH`
- URI: `/api/admin/system/role`
- 修改角色状态

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 角色流水号 | Y | 流水号 | 1 |
| `status` | 状态 | Y | 状态 | 启用：1, 禁用：2, 作废：99 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.6.取得使用者列表

- HttpMethod: `GET`
- URI: `/api/admin/system/user`
- API 将依搜寻条件搜寻出系统使用者

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `userName` | 使用者名称 |   | 使用者名称 | jb12345 |
| `roleId` | 角色 Id |   | 角色的流水号, 参考角色下拉选单 | 12 |
| `status` | 使用者状态 |  | 使用者状态 | 关闭 : 0 , 启用 : 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 使用者Id |   | 使用者的流水号 | 123 |
| `userName` | 使用者名称 | Y | 使用者名称 | jb12345 |
| `status` | 使用者状态 | Y | 使用者状态 | 0 : 关闭, 1 : 启用 |
| `createdAt` | 建立时间 | Y | 建立时间 | yyyy/MM/dd HH:mm:ss |
| `createdByUserName` | 建立者 userName | Y | 建立者 Id | jb12345 |
| `userRoles` | 使用者角色 | Y | 角色id的集合 | {4,5,10} |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.7.新增使用者

- HttpMethod: `POST`
- URI: `/api/admin/system/user`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `userName` | 使用者名称 | Y | 使用者名称 | jb12345 |
| `password` | 密码 | Y | 密码 |  |
| `roleId` | 角色 Id | Y | 角色的流水号(一或多笔） | {1,5,7} |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.8.取得使用者资料

- HttpMethod: `GET`
- URI: `/api/admin/system/user`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 使用者Id |   | 流水号 | 1 |

</div>

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 使用者Id |   | 使用者的流水号 | 123 |
| `userName` | 使用者名称 | Y | 使用者名称 | jb12345 |
| `status` | 使用者状态 | Y | 使用者状态 | 0 : 关闭, 1 : 启用 |
| `createdAt` | 建立时间 | Y | 建立时间 | yyyy/MM/dd HH:mm:ss |
| `createdByUserName` | 建立者 userName | Y | 建立者 Id | jb12345 |
| `userRoles` | 使用者角色 | Y | 角色id的集合 | {4,5,10} |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.9.修改使用者

- HttpMethod: `PUT`
- URI: `/api/admin/system/user`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 使用者Id | Y | 使用者的流水号 | 123 |
| `userName` | 使用者名称 | Y | 使用者名称 | jack |
| `roleId` | 角色名称 | Y | 角色的Id(一或多笔） | {"1","2","3"} |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.10.使用者停用/启用

- HttpMethod: `PATCH`
- URI: `/api/admin/system/user`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 使用者Id | Y | 使用者的流水号 | 123 |
| `status` | 使用者状态 | Y | 使用者状态 | 关闭 : 0 , 启用 : 1 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.11.支付渠道列表

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentchannel`
- API 将依搜寻条件搜寻出支付渠道

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 名称 |  | 支付渠道名称模糊搜寻 | 樱桃 灌钱 |
| `providerId` | 支付商Id |  | 支付商唯一Id | 4 |
| `paymentType` | 支付类型 |  | 支付类型 | 5 |
| `paymentMethod` | 支付方式 |  | 支付方式 | 6 |
| `status` | 状态 |  | 状态唯一代码 | 7 |
| `paymentPlatform` | 支付平台 |  | 支付平台 | 8 |
| `merchantId` | 商户Id |  | 商户流水号 | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付渠唯一流水号 | 1 |
| `name` | 名称 | Y | 支付渠道名称 | 樱桃 灌钱 |
| `merchantName` | 商户名称 | Y | 商户名称 | RayBet |
| `providerName` | 支付商 | Y | 支付商名称 | JetPay |
| `paymentPlatformName` | 支付平台 | Y | 支付平台名称 | 手机 |
| `paymentTypeName` | 支付类型 | Y | 支付类型名称 | 存款 |
| `paymentMethodName` | 支付方式 | Y | 支付方式名称 | 支付宝 |
| `totalLimit` | 当前周期收款金额 | Y | 当前周期收款金额 | 100.00 |
| `minDepositAmount` | 最低存款 | Y | 最低存款金额 | 100.00 |
| `maxDepositAmount` | 最高存款 | Y | 最高存款金额 | 3000.00 |
| `lastDepostAt` | 最后存款时间 |  | 最后存款时间 | 2018/09/12 17:41:53 |
| `status` | 状态 | Y | 显示目前状态, 可进行切换 | 0 : 关闭, 1 : 启用 |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.12.新增支付渠道

- HttpMethod: `POST`
- URI: `/api/admin/system/paymentchannel`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 名称 | Y | 支付渠道名称 | 樱桃 灌钱 |
| `merchantId` | 商户Id | Y | 商户流水号 | 1 |
| `paymentType` | 支付类型 | Y | 支付类型 | 5 |
| `paymentMethod` | 支付方式 | Y | 支付方式 | 6 |
| `paymentProviderId` | 支付商Id | Y | 支付商唯一Id | 4 |
| `commissionPercentage` | 手续费百分比 |  | 支付商唯一Id | 0.0140 |
| `merchantUsername` | 支付商家用户名 | Y | 支付商家用户名 | JDUG999 |
| `merchantKey` | 商家密钥 | Y | 商家密钥 | JDUG999 |
| `status` | 状态 | Y | 状态唯一代码 | 7 |
| `paymentPlatform` | 支付平台 | Y | 支付平台 | JDUG999 |
| `commissionConstants` | 手续费固定数值 |  | 手续费固定数值 | 30.00 |
| `MaxAmount` | 最高额度 | Y | 最高额度 | 3000.00 |
| `MinAmount` | 最低额度 | Y | 最低额度 | 100.00 |
| `totalLimit` | 存款上限 | Y | 存款上限 | 100.00 |
| `minimumWithdrawInterval` | 最低提款区间 | Y | 最低提款区间 | 100.00 |
| `commissionMinValue` | 手续费最低数值 |  | 手续费最低数值 | 100.00 |
| `requestUrl` | 请求地址 | Y | 请求支付商家的地址 | http://120.79.25.23/pp |
| `callbackUrl` | 回调地址 | Y | 支付商家的回调地址 | http://210.99.95.55/qq |
| `queryUrl` | 查询地址 | Y | 支付商家的查询地址 | http://111.99.95.55/pp |
| `assemblyName` | 组件名称 | Y | 组件名称 | QT |
| `handlerType` | HandlerType | Y | HandlerType | AP.Payment.JetPay.JetPayDepositHandler |
| `arguments` | 参数 |  | 参数 | {'QRCodeStyle':'Redirect'} |
| `notes` | 备注 |  | 备注 | Y |
| `extensionRoute` | ExtensionRoute | Y | 参考Extension下拉选单 | 1 |
| `callbackSuccessType` | 回调成功讯息 | Y | 参考回调成功讯息下拉选单 | 1 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.13.修改支付渠道

- HttpMethod: `PUT`
- URI: `/api/admin/system/paymentchannel`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付渠唯一流水号 | 1 |
| `name` | 名称 | Y | 支付渠道名称 | 樱桃 灌钱 |
| `merchantId` | 商户Id | Y | 商户流水号 | 1 |
| `paymentType` | 支付类型 | Y | 支付类型 | 5 |
| `paymentMethod` | 支付方式 | Y | 支付方式 | 6 |
| `paymentProviderId` | 支付商Id | Y | 支付商唯一Id | 4 |
| `commissionPercentage` | 手续费百分比 |  | 支付商唯一Id | 0.0140 |
| `merchantUsername` | 支付商家用户名 | Y | 支付商家用户名 | JDUG999 |
| `merchantKey` | 商家密钥 | Y | 商家密钥 | JDUG999 |
| `status` | 状态 | Y | 状态唯一代码 | 7 |
| `paymentPlatform` | 支付平台 | Y | 支付平台 | JDUG999 |
| `commissionConstants` | 手续费固定数值 |  | 手续费固定数值 | 30.00 |
| `MaxAmount` | 最高额度 | Y | 最高额度 | 3000.00 |
| `MinAmount` | 最低额度 | Y | 最低额度 | 100.00 |
| `totalLimit` | 存款上限 | Y | 存款上限 | 100.00 |
| `minimumWithdrawInterval` | 最低提款区间 | Y | 最低提款区间 | 100.00 |
| `commissionMinValue` | 手续费最低数值 |  | 手续费最低数值 | 100.00 |
| `requestUrl` | 请求地址 | Y | 请求支付商家的地址 | http://120.79.25.23/pp |
| `callbackUrl` | 回调地址 | Y | 支付商家的回调地址 | http://210.99.95.55/qq |
| `queryUrl` | 查询地址 | Y | 支付商家的查询地址 | http://111.99.95.55/pp |
| `assemblyName` | 组件名称 | Y | 组件名称 | QT |
| `handlerType` | HandlerType | Y | HandlerType | AP.Payment.JetPay.JetPayDepositHandler |
| `arguments` | 参数 |  | 参数 | {'QRCodeStyle':'Redirect'} |
| `notes` | 备注 |  | 备注 | Y |
| `extensionRoute` | ExtensionRoute | Y | 参考Extension下拉选单 | 1 |
| `callbackSuccessType` | 回调成功讯息 | Y | 参考回调成功讯息下拉选单 | 1 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.14.支付渠道详情

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentchannel`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付渠道Id | Y | 流水号 | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付渠唯一流水号 | 1 |
| `name` | 名称 | Y | 支付渠道名称 | 樱桃 灌钱 |
| `merchantId` | 商户Id | Y | 商户流水号 | 1 |
| `paymentType` | 支付类型 | Y | 支付类型 | 5 |
| `paymentMethod` | 支付方式 | Y | 支付方式 | 6 |
| `paymentProviderId` | 支付商Id | Y | 支付商唯一Id | 4 |
| `commissionPercentage` | 手续费百分比 | Y | 支付商唯一Id | 0.0140 |
| `merchantUsername` | 支付商家用户名 | Y | 支付商家用户名 | JDUG999 |
| `merchantKey` | 商家密钥 | Y | 商家密钥 | JDUG999 |
| `status` | 状态 | Y | 状态唯一代码 | 7 |
| `paymentPlatform` | 支付平台 | Y | 支付平台 | JDUG999 |
| `commissionConstants` | 手续费固定数值 | Y | 手续费固定数值 | 30.00 |
| `MaxAmount` | 最高额度 | Y | 最高额度 | 3000.00 |
| `MinAmount` | 最低额度 | Y | 最低额度 | 100.00 |
| `totalLimit` | 存款上限 | Y | 存款上限 | 100.00 |
| `minimumWithdrawInterval` | 最低提款区间 | Y | 最低提款区间 | 100.00 |
| `commissionMinValue` | 手续费最低数值 | Y | 手续费最低数值 | 100.00 |
| `requestUrl` | 请求地址 | Y | 请求支付商家的地址 | http://120.79.25.23/pp |
| `callbackUrl` | 商户回调地址 | Y | 支付中心回调至商户的地址 | http://210.99.95.55/qq |
| `queryUrl` | 查询地址 | Y | 支付商家的查询地址 | http://111.99.95.55/pp |
| `paymentCenterCallbackUrl` | 支付中心回调地址 | Y | 支付商回调至支付中心的地址（不能修改只供读取） | http://111.99.95.55/pp |
| `assemblyName` | 组件名称 | Y | 组件名称 | QT |
| `handlerType` | HandlerType | Y | HandlerType | AP.Payment.JetPay.JetPayDepositHandler |
| `arguments` | 参数 |  | 参数 | {'QRCodeStyle':'Redirect'} |
| `notes` | 备注 | Y | 备注 |  |
| `extensionRoute` | ExtensionRoute | Y | ExtensionRoute | 1 |
| `callbackSuccessType` | 回调成功讯息 | Y | 回调成功讯息 | 1 |



</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.15.支付渠道停用/启用/作废

- HttpMethod: `PATCH`
- URI: `/api/admin/system/paymentchannel`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付渠道Id | Y | 支付渠道 | 1 |
| `status` | 支付渠道状态 | Y | 从状态选单选取 | 启用：1, 禁用：2, 作废：99 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---


#### 4.16.取得支付渠道成功率

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentchannel/successRate`
- API 将依支付渠道Id取得支付成功率

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付渠道Id | Y | 流水号 | 1 |
| `successRateDateType` | 成功率计算日期 |  | 参照下拉选单 | 1 |
| `date` | 日期 |  | 使用月历挑选日期 | yyyy/MM/dd |
| `month` | 月份 |  | 使用月历挑选月份 | yyyy/MM |


</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付渠道Id | Y | 支付渠道Id | 3 |
| successRates | 成功率 | Y | 成功率(%) | 85.50 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.17.银行总表列表

- HttpMethod: `GET`
- URI: `/api/admin/system/bank`
- API 将依搜寻条件搜寻银行总表

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 银行名称 |  | 银行名称模糊搜寻 | 中国银行 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 银行唯一流水号 | 1 |
| `name` | 名称 | Y | 银行名称 | 中国银行 |
| `code` | 编码 | Y | 银行编码 | YCZY |
| `url` | 网址 |  | 银行网站 | http://www.abchina.com/cn/ |
| `createdAt` | 创建时间 | Y | 资料建立时间 | 2018/06/13 10:26:21 |
| `createdById` | 创建人 | Y | 建立资料的使用者 | John |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.18.新增银行总表

- HttpMethod: `POST`
- URI: `/api/admin/system/bank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 名称 | Y | 银行名称 | 中国银行 |
| `code` | 编码 | Y | 银行编码 | YCZY |
| `url` | 网址 |  | 银行网站 | http://www.abchina.com/cn/ |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.19.取得银行总表详细

- HttpMethod: `GET`
- URI: `/api/admin/system/bank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 银行唯一流水号 | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 银行唯一流水号 | 1 |
| `name` | 名称 | Y | 银行名称 | 中国银行 |
| `code` | 编码 | Y | 银行编码 | YCZY |
| `url` | 网址 |  | 银行网站 | http://www.abchina.com/cn/ |
| `createdAt` | 创建时间 | Y | 资料建立时间 | 2018/06/13 10:26:21 |
| `createdById` | 创建人 | Y | 建立资料的使用者 | John |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.20.修改银行总表

- HttpMethod: `PUT`
- URI: `/api/admin/system/bank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 银行唯一流水号 | 1 |
| `name` | 名称 | Y | 银行名称 | 中国银行 |
| `code` | 编码 | Y | 银行编码 | YCZY |
| `url` | 网址 |  | 银行网站 | http://www.abchina.com/cn/ |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.21.支付服务商列表

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentProvider`
- API 将依搜寻条件搜寻支付服务商

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 服务商名称 |  | 服务商名称 | 鑫宝付 |
| `status` | 状态 |  | 从状态选单选取 |  启用：1, 禁用：2, 作废：99  |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付服务商唯一流水号 | 1 |
| `name` | 服务商名称 | Y | 服务商名称 | 鑫宝付 |
| `createAt` | 创建时间 | Y | 资料建立时间 | 2018/06/13 10:26:21 |
| `createdById` | 创建人 | Y | 建立资料的使用者 | John |
| `status` | 状态 | Y | 状态 |  启用：1, 禁用：2, 作废：99  |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.22.新增支付服务商

- HttpMethod: `POST`
- URI: `/api/admin/system/paymentProvider`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 服务商名称 | Y | 服务商名称 | 鑫宝付 |
| `merchantId` | 商戶Id | Y | 參考商戶下拉選單 Merchant | 1 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.23.取得支付服务商详细

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentProvider`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付服务商唯一流水号 | 1 |
| `merchantId` | 支付商Id | Y | 支付商流水号 | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付服务商唯一流水号 | 1 |
| `name` | 服务商名称 | Y | 服务商名称 | 鑫宝付 |
| `createAt` | 创建时间 | Y | 资料建立时间 | 2018/06/13 10:26:21 |
| `createdById` | 创建人 | Y | 建立资料的使用者 | John |
| `status` | 状态 | Y | 状态 |  启用：1, 禁用：2, 作废：99  |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.24.修改支付服务商

- HttpMethod: `PUT`
- URI: `/api/admin/system/paymentProvider`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付服务商唯一流水号 | 1 |
| `name` | 服务商名称 | Y | 服务商名称 | 鑫宝付 |
| `merchantId` | 支付商Id | Y | 支付商流水号 | 1 |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.25.支付服务商停用/启用

- HttpMethod: `PATCH`
- URI: `/api/admin/system/paymentProvider`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 服务商名称 | Y | 服务商名称 | 鑫宝付 |
| `status` | 状态 | Y | 状态 |  启用：1, 禁用：2, 作废：99  |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.26.支付银行列表

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentProviderBank`
- API 将依搜寻条件搜寻支付银行

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `name` | 服务商名称 |  | 服务商名称 | 鑫宝付 |
| `paymentMethodId` | 支付方式 |  | paymentMethod 下拉选单 | 4 |
| `paymentTypeId` | 支付类型Id |  | paymentType 下拉选单 | 3 |
| `status` | 状态 |  | 从状态选单选取 |  启用：1, 禁用：2, 作废：99  |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付银行唯一流水号 | 4 |
| `paymentProviderBankName` | 银行名称 | Y | 银行名称 | 交通银行 |
| `paymentProviderName` | 服务商 | Y | 服务商名称 | 鑫宝付 |
| `paymentTypeName` | 支付类型 | Y | 支付类型 | 提款 |
| `paymentMethodName` | 支付方式 | Y | 支付方式 | 网银支付 |
| `paymentProviderBankCode` | 支付商银行代码 | Y | 支付商银行代码 | CMBC |
| `status` | 状态 | Y | 状态 |  启用：1, 禁用：2, 作废：99  |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.27.新增支付银行

- HttpMethod: `POST`
- URI: `/api/admin/system/paymentProviderBank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `bankId` | 银行Id | Y | 从银行选单取得 | 1 |
| `merchantId` | 支付商Id | Y | 支付商流水号 | 1 |
| `paymentMethodId` | 支付类型Id | Y | 从支付类型选单取得 | 2 |
| `paymentProviderId` | 服务商Id | Y | 从服务商选单取得 | 3 |
| `paymentMethodId` | 支付方式Id | Y | 从支付方式选单取得 | 4 |
| `paymentProviderBankCode` | 支付商银行代码 | Y | 支付商银行代码 | CMBC |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.28.取得支付银行详细

- HttpMethod: `GET`
- URI: `/api/admin/system/paymentProviderBank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付银行唯一流水号 | 4 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 支付银行唯一流水号 | 4 |
| `paymentProviderBankName` | 银行名称 | Y | 银行名称 | 交通银行 |
| `paymentProviderId` | 服务商Id | Y | 从服务商选单取得 | 1 |
| `paymentTypeId` | 支付类型Id | Y | 从支付类型选单取得 | 2 |
| `paymentMethodId` | 支付方式Id | Y | 从支付方式选单取得 | 3 |
| `paymentProviderBankCode` | 支付商银行代码 | Y | 支付商银行代码 | CMBC |
| `status` | 状态 | Y | 状态 |  启用：1, 禁用：2, 作废：99  |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.29.修改支付银行

- HttpMethod: `PUT`
- URI: `/api/admin/system/paymentProviderBank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付银行流水号 | Y | 支付银行唯一流水号 | 1 |
| `bankId` | 银行Id | Y | 从银行选单取得 | 1 |
| `merchantId` | 支付商Id | Y | 支付商流水号 | 1 |
| `paymentMethodId` | 支付类型Id | Y | 从支付类型选单取得 | 2 |
| `paymentProviderId` | 服务商Id | Y | 从服务商选单取得 | 3 |
| `paymentTypeId` | 支付方式Id | Y | 从支付方式选单取得 | 4 |
| `paymentProviderBankCode` | 支付商银行代码 | Y | 支付商银行代码 | CMBC |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.30.支付银行停用/启用

- HttpMethod: `PATCH`
- URI: `/api/admin/system/paymentProviderBank`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付银行流水号 | Y | 支付银行唯一流水号 | 1 |
| `status` | 状态 |  | 从状态选单选取 |  启用：1, 禁用：2, 作废：99  |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.31.业务日志

- HttpMethod: `GET`
- URI: `/api/admin/system/entitylog`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `targetType` | 类型 |  | 参考EntityLogTargetType下拉单 | 1 |
| `targetId` | Id |  | targetId |  123  |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `targetType` | 类型 | Y | 类型名称 | QQ钱包存款 |
| `targetId` | Id | y | targetId |  123  |
| `content` | 内容 | y | Log内容 |  正在发送存款支付请求  |
| `createdAt` | 创建时间 | y | 创建时间 |  yyyy/MM/dd HH:mm:ss  |
| `feature` | 可使用的功能列表 | Y | 功能列表 | { "isEnableEdit": true, "isEnableDetail": false, "isEnableManual": true, "isEnableQuery": false } |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

#### 4.32.业务日志详情

- HttpMethod: `GET`
- URI: `/api/admin/system/entitylog`

### Request
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | id | Y | EntityLog 唯一流水号 | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `details` | 详情 | Y | 记录errLog等等资讯 |  |

</div>

>> [系統管理相关](#4系統管理相关) | [索引](#索引)

---

### 5.系統功能相关

#### `重点内容`

[5.1.取得功能列表](#51取得功能列表)

[5.2.取得支付商选单](#52取得支付商选单)

[5.3.取得支付类型选单](#53取得支付类型选单) 

[5.4.取得支付方式选单](#54取得支付方式选单) 

[5.5.取得状态选单](#55取得状态选单) 

[5.6.取得支付平台选单](#56取得支付平台选单) 

[5.7.取得订单状态选单](#57取得订单状态选单)

[5.8.取得支付渠道选单](#58取得支付渠道选单)

[5.9.取得角色选单](#59取得角色选单)

[5.10.取得日志类型选单](#510取得日志类型选单)

[5.11.取得商户选单](#511取得商户选单)

[5.12.取得银行选单](#512取得银行选单)

[5.13.取得延伸路径选单](#513取得延伸路径选单)

[5.14.取得回传讯息选单](#514取得回传讯息选单)

[5.15.取得提款订单状态选单](#515取得提款订单状态选单)

[5.16.取得提款支付渠道选单](#516取得提款支付渠道选单)

[5.17.取得灌钱银行卡选单](#517取得灌钱银行卡选单)

[5.18.取得灌钱通道选单](#518取得灌钱通道选单)

---

#### 5.1.取得功能列表

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/permissiongroup`
- API 取得页面上的功能列表

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 功能流水号 | Y | 流水号 | 1 |
| `name` | 功能名称 | Y | 角色名称 | 客服主管 |
| `subPermissionGroups` | 子功能目录 | Y | 树状结构列出 | [ {"id":"1", "name":"name1", "subPermissionGroups":[], "permissions":[{"id1":"1", "name1":"permission1"}]}, {"id":"2", "name":"name2", "subPermissionGroups":[], "permissions":[]} ] |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.2.取得支付商选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/PaymentProvider`
- API 将会取得所有启用中的支付商

### Response

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付商唯一的代码 | 1 |
| `name` | 支付商名称 | Y | 支付商名称 | FP网银 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.3.取得支付类型选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/PaymentType`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付类型唯一的代码 | 1 |
| `name` | 支付类型名称 | Y | 支付类型名称 | 存款 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.4.取得支付方式选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/PaymentMethod`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付方式唯一的代码 | 1 |
| `name` | 支付方式名称 | Y | 支付方式名称 | 支付宝 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.5.取得状态选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/EntityStatus`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该状态的代码 | 1 |
| `name` | 状态名称 | Y | 状态名称 | 启用 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.6.取得支付平台选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/PaymentPlatform`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付平台的代码 | 1 |
| `name` | 支付平台名称 | Y | 支付平台名称 | 电脑 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.7.取得订单状态选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/DepositStatus`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付平台的代码 | 1 |
| `name` | 订单状态名称 | Y | 订单状态名称 | 到帐 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.8.取得支付渠道选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/PaymentChannel`
- API 将依 paymentMethod 取得所有支付渠道

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付方式id | Y | 支付方式id | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付方式唯一的代码 | 1 |
| `name` | 支付方式名称 | Y | 支付方式名称 | 支付宝 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.9.取得角色选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/Role`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该角色唯一的代码 | 1 |
| `name` | 角色名称 | Y | 角色名称 | Administrator |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.10.取得日志类型选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/EntityLogTargetType`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该角色唯一的代码 | 1 |
| `name` | 类型名称 | Y | 类型名称 | 支付宝存款 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.11.取得商户选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/Merchant`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该商户唯一的代码 | 1 |
| `name` | 商户名称 | Y | 商户名称 | rb |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.12.取得银行选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/Bank`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该银行唯一的代码 | 1 |
| `name` | 银行名称 | Y | 银行名称 | 工商银行 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.13.取得延伸路径选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/ExtensionRoute`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 流水号 | 1 |
| `name` | 名称 | Y | 名称 | JBP |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.14.取得回传讯息选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/CallbackSuccessType`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 流水号 | 1 |
| `name` | 讯息 | Y | 讯息 | SUCCESS |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.15.取得提款订单状态选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/WithdrawalStatus`

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付平台的代码 | 1 |
| `name` | 订单状态名称 | Y | 订单状态名称 | 到帐 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.16.取得提款支付渠道选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/WithdrawalPaymentChannel`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 支付类型id | Y | 支付类型id | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该支付方式唯一的代码 | 1 |
| `name` | 支付方式名称 | Y | 支付方式名称 | 支付宝 |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---

#### 5.17.取得灌钱银行卡选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/internalbankcard`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户Id | Y | 商户号唯一Id | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该银行卡唯一的代码 | 1 |
| `name` | 灌钱银行卡名称 | Y | 灌钱银行卡名称 |  |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---


#### 5.18.取得灌钱通道选单

- HttpMethod: `GET`
- URI: `/api/admin/systemextension/options/internalpaymentchannel`

### Request

{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `merchantId` | 商户Id | Y | 商户号唯一Id | 1 |

</div>

### Response
{::options parse_block_html="true" /}

<div>
  
|参数|参数名称|必填|说明|举例|
|:------------:|:---------:|:---:|:-------------:|:-------:|
| `id` | 流水号 | Y | 代表该灌钱通道唯一的代码 | 1 |
| `name` | 灌钱通道名称 | Y | 灌钱通道名称 |  |

</div>

>> [系統功能相关](#5系统功能相关) | [索引](#索引)

---
