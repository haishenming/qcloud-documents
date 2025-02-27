## 概述
TDMQ CMQ 版目前支持 Java、Python、PHP 及 C++ SDK ，后续会支持更多语言。欢迎广大开发者根据 API 说明开发更多语言版本的 SDK。
由于分配资源和释放资源需要1s左右的时间，当前消息队列 SDK 在创建及删除队列/主题时会有1s延迟，建议在程序中增加创建和删除的时间间隔保障调用成功。

## 下载地址

不同语言版本 SDK 的 GitHub 地址如下：
- [Java SDK](https://github.com/tencentyun/cmq-java-sdk)
- [Python SDK](https://github.com/tencentyun/cmq-python-sdk)（默认为 Python2 SDK，您可切换至 Python3 分支中查看 Python3 SDK ）
- [PHP SDK](https://github.com/tencentyun/cmq-php-sdk)
- [C++ SDK](https://github.com/tencentyun/cmq-cpp-sdk)

## 注意事项
使用 SDK 前至少要获取 [SecretId](https://console.cloud.tencent.com/capi)、 [SecretKey](https://console.cloud.tencent.com/capi) 和 API接入地址（即请求发到哪个地域，走内网还是外网）。API 接入地址说明如下。

#### 队列模型
**请参照下面说明将域名中的 {$region} 替换成相应地域：**

- 外网接口请求域名：`https://cmq-{$region}.public.tencenttdmq.com`
- 内网接口请求域名：`http://{$region}.mqadapter.cmq.tencentyun.com`


#### 主题模型 [](id:topic)
**请参照下面说明将域名中的 {$region} 替换成相应地域：**
- 外网接口请求域名：`https://cmq-{$region}.public.tencenttdmq.com`
- 内网接口请求域名：`http://{$region}.mqadapter.cmq.tencentyun.com`

如果业务进程也部署在腾讯云的 CVM 子机上，强烈建议使用同地域的内网接入。例如：在腾讯云北京地域的 CVM 子机，则建议您使用 `http://bj.mqadapter.cmq.tencentyun.com`。原因如下：
- 同地域内网时延更低。
- 目前消息队列对于公网下行流量是要收取流量费用的，用内网可以节省这部分的费用。

#### 说明
{$region}需用具体地域替换：gz（广州），sh（上海），bj（北京），hk（中国香港），cd（成都）。公共参数中的 region 值要与域名的 region 值保持一致，如果出现不一致的情况，以域名的 region 值为准，将请求发往域名 region 所指定的地域。


## Demo工程使用
### 准备 Demo 环境
1. **安装 IDEA**
您可以安装 IntelliJ IDEA 或者 Eclipse，本文以 IntelliJ IDEA 为例进行说明。
请在 [下载 IntelliJ IDEA Ultimate 版本](https://www.jetbrains.com/idea/)，并参考 IntelliJ IDEA 说明进行安装。
2. **下载 Demo 工程**
请在 [下载 TDMQ CMQ 版 HTTP 的 Demo 工程](https://github.com/tencentyun/cmq-java-sdk) 到本地，解压后即可看到本地新增的 cmq-java-sdk-master 文件夹。


### 配置 Demo 工程
1. **创建资源**
您需要在控制台创建所需消息队列资源，包括 TDMQ CMQ 版队列名、SecretID、SecretKey。
具体创建过程请参考 [队列模型快速入门](https://cloud.tencent.com/document/product/1496/61006)。
2. **导入 Demo 工程文件**
在 IDEA 的开机界面打开文件夹。
![](https://main.qcloudimg.com/raw/8a3ba96ef290ad50f6f0d20c01594f5d.png)
打开文件夹后，Demo 工程文件存于`/src/main/java/com/qcloud/cmq/example`文件夹下。
3. **配置 Demo 参数**
修改文件请求地址、密钥对等。以 Producer 为例，配置如下：
```java
String secretId="获取的SecretID";
String secretKey="获取的SecretKey";
String endpoint = "https://****.com";
String queueName = "test";
```
选择“新建队列”和“使用已有队列”：
```java
//创建新队列并设置属性
QueueMeta meta = new QueueMeta();
meta.pollingWaitSeconds = 10;
meta.visibilityTimeout = 10;
meta.maxMsgSize = 1048576;
meta.msgRetentionSeconds = 345600;
Queue queue = account.createQueue(queueName,meta);
```
```java
//使用控制台已有队列
Queue queue = account.getQueue(queueName);
```
本 Demo 使用的是当前账号已有队列，如需选择新建队列，修改 queueName 为将要创建的队列名，然后找到新建队列相关代码取消注释。
注释代码均为常用操作，“删除”操作需谨慎使用，其他类中的配置参考 Producer 类。

### 运行 Demo
#### 使用队列模型收发消息
先运行 Producer 类发送消息，再运行 Consumer 类接受消息。  
发送消息代码示例：
```java
String msg = "hello!";
String msgId = queue.sendMessage(msg);
System.out.println("==> send success! msg_id:" + msgId);
```
接收消息代码示例：
```java
Message msg = queue.receiveMessage(10);
```
#### 使用主题模型收发消息
运行 TopicDemo 类，主题模型请求域名参考 [主题模型请求域名](#topic)。  
发布消息示例：

```java
String msg = "hello!";
String msgId = topic.publishMessage(msg);
```
处理消息示例：
```java
String queueName = "test";
String subscriptionName = "sub-test";
String Endpoint = queueName;
String Protocol = "queue";
account.createSubscribe(topicName,subscriptionName, Endpoint, Protocol);
```
创建订阅者时填写一个队列，用队列处理消息。
