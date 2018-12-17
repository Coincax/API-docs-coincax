入门指引<br>
===
API概述<br>
-----
Coincax接口是提供服务的基础，开发者在Coincax网站创建账号后，可以根据自身需求建立不同权限的API，并利用API进行自动交易。<br>
通过API可以快速实现以下功能：<br>
* 1.查询可用和冻结金额<br>
* 2.查询自己当前尚未成交的挂单<br>
* 3.快速买进卖出撤单<br>
* 4.查询历史记录<br>
* 5.查询币种行情<br>
* 6.查询K线数据<br>

API权限
<br>
--
用户的API权限需要发送邮件到coincax官方邮箱进行申请。其中api_key是提供给API用户的访问密钥，api_secret用于对请求参数签名的私钥。<br>
##注意： 请勿向任何人泄露这两个参数，这两个参数关乎您账号的安全。##<br>

签名
<br>
---
用户提交的参数除sign外都需要参与签名。<br>签名规则：首先将待签名字符串添加私钥按照参数进行升序排序。<br>
例如：对于如下的参数进行签名(下单交易)<br>
`String[] parameters= {"jbaaaaaaaa", "EOS_ETH", "1", "0.00731001", "48.6", "484001531279255241", "feefefdafdfefsfdsfe"}。`<br>
生成待签名的字符串<br>
`"0.00731001148.6484001531279255241GTB_ETHfeefefdafdfefsfdsfejbaaaaaaaa"。`<br>
最后将字符串进行SHA1加密，得到最终的字符串<br>
`"6454ed40e1db21a57f477f482584adc2f41d5c9d"（该字符串赋值于参数sign）`。<br>
