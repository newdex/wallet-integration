# 钱包集成文档

## 集成说明
Newdex需要钱包提供一些必要的接口以进行交互。接口必须注入到Window的scatter变量中。具体接口请看下面的列表。

## 需要的接口列表

### 事件 scatterLoaded
当钱包往页面注入JS完成后，需要触发一个CustomEvent，名称为"scatterLoaded"

### 方法 scatter.getIdentity(networks)
说明：获取钱包的当前账号信息
参数：networks，示例如下
```
{
    accounts: [{
        blockchain: 'eos',
        protocol: 'https',
        host: 'eos.newdex.one',
        port: 443,
        chainId: 'aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906'
    }]
}
```
返回：返回Promise对象，得到的正常的结果示例如下
```
{
    accounts: [{
        authority: "active"
        blockchain: "eos"
        chainId: "aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906"
        isHardware: false
        name: "newdexiotest"
        publicKey: "EOS5C7eh8CD9KqYETumPFjRjYaZrzPtQ8xt5uYY8XuTFZRRS8Sm1P"
    }],
    hash: "a7d14118a71c163f2bd0c7e6bc52ced2"
    kyc: false
    name: "default"
    publicKey: "EOS8KAnYVnhZQ4HG8W9N8iTDpy6NDG3Y2ob48BGQbre8J1HBWt51c"
}
```

### 方法 scatter.forgetIdentity()
说明：退出登录

### 方法 scatter.eos(network, Eos, eosOptions)
说明：获取Eos对象

参数：network，同上说明
参数：Eos，就是eosjs类（v16.0.9）  
参数：eosOptions，这是一些eos对应的配置项

返回：返回实例化的eos对象，Newdex可以用此对象直接执行eos.transcation(...)方法并调出授权界面  

### 方法 scatter.getArbitrarySignature(publicKey, data)

钱包通过提供的publicKey配对的私钥来对data内容进行签名

返回直接是签名的结果

