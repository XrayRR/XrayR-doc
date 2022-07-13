# 基本对接配置

1. 在`config.yml`中配置`PanelType: "V2board"`。
2. V2board只有V2ray节点类型支持面板配置审计规则，其他协议请使用XrayR[本地审计功能](../gong-neng-shuo-ming/rule.md)。
3. 启用vless和xtls，请在配置文件中手动启动，V2board不支持在线配置，同时V2board不支持vless和xtls下发，请手动修改客户端配置，或者自行寻找其他解决方案。

配置文件详见：[配置文件说明](../xrayr-pei-zhi-wen-jian-shuo-ming/config.md)

### 对接vmess+ws
v2board需要在传输协议配置中增加以下内容，配置ws的路径：
```
{
  "path": "/name",
}
```
其中`"name"`换成任意字符串，可用于nginx等反代分流。

### 对接vmess+grpc

为了成功支持clash连接，在对接vmess+grpc时，v2board需要在传输协议配置中增加如下内容：

```text
{
  "serviceName": "name",
}
```

其中`"name"`换成任意字符串，可用于nginx等反代分流。

### 对接vmess+tcp+http

{% hint style="info" %}
原生V2board不支持tcp+http订阅下发，请自行寻找解决方法，或手动配置客户端文件。
{% endhint %}

在对接vmess+tcp+http时，v2board需要在传输协议配置中增加如下内容：

```text
{
  "header": {
    "type": "http",
    "request": {},
    "response": {}
  }
}
```

其中`request`和`response`中的内容请自行参照[Xray-core文档](https://xtls.github.io/config/transports/tcp.html#httpheaderobject)设置。

