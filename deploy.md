# APO中的网络节点和部署

## 1 超级节点

### 1.1超级节点介绍
超级节点(简称SN)是APO网络上的记账人，一共3个，负责对网络上广播出来的交易数据进行验证，并将交易打包进区块中，他们是轮流的方式打包区块。超级代表的信息是在APO网络上公开的，所有人都可以获取这些信息。
### 1.2超级节点部署方式
```
java -jar FullNode.jar -p your privatekey --witness -c your config.conf(Example：见同目录下的beta.config.conf)
Example:
Java -jar FullNode.jar -p 650950B193DDDDB35B6E48912DD28F7AB0E7140C1BFDEFD493348F02295BD812 --witness -c ./config.conf
```
### 1.3建议硬件配置
最低配置要求：
CPU：16核 内存：32G 带宽：100M 硬盘：1T
推荐配置要求：
CPU：64核及以上 内存：64G及以上 带宽：500M及以上 硬盘：20T及以上
## 2 全节点
### 2.1 全节点介绍
FullNode是拥有完整区块链数据的节点，能够实时更新数据，负责交易的广播和验证，提供操作区块链的api和查询数据的api。
### 2.2 全节点部署方式
```
java  -jar FullNode.jar  -c your config.conf(Example：见附录)
Example:
Java -jar FullNode.jar  ./config.conf
```
### 2.3 建议硬件配置


最低配置要求：
CPU：16核 内存：32G 带宽：100M 硬盘：1T

推荐配置要求：
CPU：64核及以上 内存：64G及以上 带宽：500M及以上 硬盘：20T及以上

## 3 申请超级节点

### 3.1 申请超级节点流程

#### 3.1.1 部署超级节点

详情参照 超级节点部署章节

#### 3.1.2 创建超级节点申请交易

```
wallet/createwitness
作用：申请成为超级代表
demo：curl -X POST  http://127.0.0.1:8080/wallet/createwitness -d '{"owner_address":"17d1e7a6bc354106cb410e65ff8b181c600ff14292", "url": "007570646174654e616d6531353330363038383733343633"}'
参数说明：owner_address是申请成为超级代表的账号地址，需要是hexString格式；url是官网地址，需要是hexString格式
返回值：申请超级代表的Transaction
```

#### 3.1.3 签名

对上面返回的交易进行签名（建议本地签名）

#### 3.1.4 交易广播

```
wallet/broadcasttransaction
作用：对签名后的transaction进行广播
demo：curl -X POST  http://127.0.0.1:8080/wallet/broadcasttransaction -d '{"signature":["97c825b41c77de2a8bd65b3df55cd4c0df59c307c0187e42321dcc1cc455ddba583dd9502e17cfec5945b34cad0511985a6165999092a6dec84c2bdd97e649fc01"],"txID":"454f156bf1256587ff6ccdbc56e64ad0c51e4f8efea5490dcbc720ee606bc7b8","raw_data":{"contract":[{"parameter":{"value":{"amount":1000,"owner_address":"17e552f6487585c2b58bc2c9bb4492bc1f17132cd0","to_address":"17d1e7a6bc354106cb410e65ff8b181c600ff14292"},"type_url":"type.googleapis.com/protocol.TransferContract"},"type":"TransferContract"}],"ref_block_bytes":"267e","ref_block_hash":"9a447d222e8de9f2","expiration":1530893064000,"timestamp":1530893006233}}'
参数说明：签名之后的Transaction
返回值：广播是否成功
```
