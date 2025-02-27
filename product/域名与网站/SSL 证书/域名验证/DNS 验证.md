
## 操作场景
本文档将指导您在证书管理控制台申请证书或新增域名资料时，并且域名验证方式为 DNS 验证，如何进行域名验证操作。

## 操作步骤

### 步骤1：查看验证信息[](id:details)
1. 登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)。
2. 选择**验证中**的证书，进入 “验证域名” 页面，并在规定时间内完成验证操作。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/364718e7fbc1afb7ea870d7c6f33952a.png)

### 步骤2：添加解析记录
>!以下操作仅针对域名对应的**域名解析商**在腾讯云的情况下，若不在腾讯云，请您到域名对应的**域名解析商**处进行解析。
>
1. 请您先找到**验证域名（步骤1图例）**页面，获取**主机记录**以及**记录值**。
2. 登录 [DNS 解析 DNSPod 管理控制台](https://console.cloud.tencent.com/cns) ，查看已申请证书的域名，并单击操作栏的**解析**，进入**记录管理**页面。如下图所示：
![](https://main.qcloudimg.com/raw/f4b3aca0b6d6fea92854bf0110c396c6.png)
3. 单击**添加记录**，并根据不同证书类型添加 DNS 记录。
>?DNS 记录仅支持 CNAME 及 TXT 记录类型，且不同记录类型适用不同的品牌证书，请结合实际情形进行选择。
>
<dx-tabs>
::: 其他品牌证书
其他品牌证书需填写记录类型为 TXT 的解析记录。如下图所示：
![](https://main.qcloudimg.com/raw/ab7f65ad2f88d607024c578329f888a4.png)
 - **主机记录**：请按照 [步骤1](#details) 执行并获取主机记录值。
 - **记录类型**：选择 “TXT”。
 - **线路类型**：选择 “默认” 类型，否则会导致 CA 机构无法进行扫描认证。
 - **记录值**：请按照 [步骤1](#details) 执行并获取记录值。
 - **MX 优先级**：不需要填写。
 - **TTL**：为缓存时间，数值越小，修改记录各地生效时间越快，默认为600秒。
:::
::: Wotrus\s品牌证书
Wotrus 品牌证书需填写记录类型为 CNAME 的解析记录。如下图所示：
![](https://main.qcloudimg.com/raw/a3b57cc3d516d7b6320af4fea47b7dd3.png)
 - **主机记录**：请按照 [步骤1](#details) 执行并获取主机记录值。
 - **记录类型**：选择 “CNAME”。
 - **线路类型**：选择 “默认” 类型，否则会导致 CA 机构无法进行扫描认证。
 - **记录值**：请按照 [步骤1](#details) 执行并获取记录值。
 - **MX 优先级**：不需要填写。
 - **TTL**：为缓存时间，数值越小，修改记录各地生效时间越快，默认为600秒。
:::
</dx-tabs>
4. 单击**保存**，完成添加。
5. 添加成功后，证书对应域名添加记录值的系统会定时检查，若 CA 机构能检测到并且与指定的值匹配，即可完成域名所有权验证，请耐心等待 CA 机构扫描审核。
>?
>- 解析生效时间一般为**10分钟 - 24小时**，但各地解析的最终生效取决于各运营商刷新时间，请您耐心等待。
>- 证书颁发完成或域名信息审核通过后，解析记录可手动清除。





