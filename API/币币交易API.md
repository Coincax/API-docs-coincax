
币币API<br>
====
请求交互<br>
--
所有访问的根URL： `https://api.coincax.com` 。所有请求基于Https协议。<br>

API参考
<br>
--
　1.POST /api/entrust/done.do 单次下单交易（访问频率 60次/2秒）<br>
    URL `https://api.coincax.com/api/entrust/done.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/entrust/done.do
Response
{
　　"code": 0,
    "langkey": "entrust_success",
    "entrust_sn": "20180702000035715049"
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
langkey：返回消息
entrust_sn:订单号
```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| symbol       	| String        |   是   |   交易对类型（EOS_ETH）    |
| trade_type  	| String   	    |   是   |   交易类型（1买入，2卖出）  |
| price		 	    | Double        |  	 是   |   下单价格                 |
| num 		    	| Double 	      |   是   |   下单数量                 |
| nonce		    	| String   	  	|   是   |   18位随机数               |
| sign   	| String   	    |   是   |   请求参数的签名            |

　2.POST /api/entrust/cancel.do    单次撤单交易（访问频率 10次/2秒）<br>
    URL `https://api.coincax.com/api/entrust/cancel.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/entrust/cancel.do
Response
{
    "code": 0,
    "entrust_sn": "20180711000035727734",
    "langkey": "cancel_success"
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
langkey：返回消息
entrust_sn:订单号
```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| entrust_sn       	| String        |   是   |   订单号    |
| nonce		    	| String   	  	|   是   |   18位随机数               |
| sign   	| String   	    |   是   |   请求参数的签名            |

<br>
--
　3.POST /api/entrust/batch_done.do 批量下单交易（访问频率 60次/2秒,单次下单量最大量50条）<br>
    URL `https://api.coincax.com/api/entrust/batch_done.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/entrust/batch_done.do
Response
{
　　"code": 0,
    "langkey": "entrust_success",
    "data": [{"code":0,"entrust_sn":"20180711000035727735"},{"code":0,"entrust_sn":"20180711000035727736"}]
}
```
返回值说明
```
code：返回状态，0成功，第一条委托下单状态,
langkey：返回消息第一条委托下单提示
data:委托结果,结果顺序和下单参数data顺序一致,code：返回状态，0成功，entrust_sn委托单号
```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| data    	  | String		    |   是   |最大量50条,值必须是json格式字符串, 例"[{"symbol":"ETH_BTC","trade_type":1,"price":"1.23","num":"2"}]",symbol交易对类型（EOS_ETH）,trade_type 交易类型（1买入，2卖出）,price下单价格,num下单数量|
| nonce		    	| String   	  	|   是   |   18位随机数               |
| sign   	| String   	    |   是   |   请求参数的签名            |

　4.POST /api/entrust/batch_cancel.do 批量撤单交易（访问频率 10次/2秒,单次撤单量最大量10条）<br>
    URL `https://api.coincax.com/api/entrust/batch_cancel.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/entrust/batch_cancel.do
Response
{
    "code": 0,
    "entrust_sns": {"20180711000035727734":-1,"20180711000035727735":-1},
    "langkey": "cancel_success"
}
```
返回值说明
```
code：返回状态，0成功，第一条委托撤销状态
langkey：返回消息，第一条委托撤销提示
entrust_sns:订单结果列表,委托单撤销状态 //委托单对应的值,撤销状态 -4格式不正确,委托单不存在,无权操作,-3撤单处理中,-2撤销失败,-1已撤销 2:完全成交

```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| entrust_sns      	| String        |   是   |  单次撤单量最大量10条,值必须是json格式字符串,["20180711000035727734","20180711000035727735"]    |
| nonce		    	| String   	  	|   是   |   18位随机数               |
| sign   	| String   	    |   是   |   请求参数的签名            |


　5.POST /api/entrustfind/notall_search.do 查询委托记录（访问频率 10次/2秒）<br>
    URL `https://api.coincax.com/api/entrustfind/notall_search.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/entrustfind/notall_search.do
Response
{
    "code": 0,
    "page": "1",
    "limit": "1000",
    "page_rows": 1000,
    "count": 1699,
    "page_total": 2,
    "list": [
        {
            "entrust_sn": "20180711000032288884",
            "trade_type": "1",
            "entrust_price": "0.01571521",
            "entrust_num": "11.65700000",
            "deal_num": "0.00000000",
            "trade_state": "0",
            "add_time": "1531334798",
            "symbol": "EOS_ETH"
        }
    ]
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
page：当前页数
limit：每页多少条数据
page_rows：当前页多少条数据
count：一共多少条数据
page_total：当前一共多少页
entrust_sn：订单号
trade_type：交易类型（1买入，2卖出）
entrust_price：委托价格
entrust_num：委托数量
deal_num：实际成交数量
trade_state：订单状态（0未成交，1部分成交，2全部成交）
add_time：委托时间
symbol：委托交易对
```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| page       	| Integer        |   是   |   当前页数    |
| symbol		    	| String   	  	|   否   |   交易对类型，默认所有，可以指定（EOS_ETH）               |
| limit   	| Integer   	    |   否   |   指定获取数据的条数（默认10条，最大500条）            |
| nonce   	| String   	    |   是   |   18位随机数            |
| sign   	| String   	    |   是   |   请求参数的签名            |

　6.POST /api/usercoin/get_balance.do 查询用户信息（访问频率 10次/2秒）<br>
    URL `https://api.coincax.com/api/usercoin/get_balance.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/usercoin/get_balance.do
Response
{
    "code": 0,
    "data": {
        "money": {
            "BTC": "1.84930465",
            "ETH": "1.68873769",
            "LTC": "1.72449999",
           
        },
        "frozen": {
            "BTC": "1.78115011",
            "ETH": "1.11742635",
            "LTC": "1.69700001",
           
        }
    }
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
money：账户余额
frozen：账户冻结余额

```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| nonce   	| String   	    |   是   |   18位随机数            |
| sign   	| String   	    |   是   |   请求参数的签名            |

　7.POST /api/entrustfind/deal_search.do 查询历史记录（访问频率 10次/2秒）<br>
    URL `https://api.coincax.com/api/entrustfind/deal_search.do`<br>
示例<br>

```
Request
POST　https://api.coincax.com/api/entrustfind/deal_search.do
Response
{
    "page": "1",
    "limit": 10,
    "page_rows": 10,
    "count": 1000,
    "page_total": 100,
    "code": 0,
    "list": [
        {
            "deal_sn": "20180712000022311348",
            "entrust_sn": "20180712000035118501",
            "trade_type": "2",
            "deal_type": "0",
            "deal_price": "0.01544642",
            "deal_num": "6.83000000",
            "deal_time": "1531385203",
            "symbol": "EOS_ETH"
        }
    ]
   
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
page：当前页数
limit：每页多少条数据
page_rows：当前页多少条数据
count：一共多少条数据
page_total：一共多少页
deal_sn：成交单号
entrust_sn：委托单号
trade_type：交易类型（1买入，2卖出）
deal_type：成交类型（1主动成交，2被动成交）
deal_price：实际成交价格
deal_num：实际成交数量
deal_time:实际成交时间
symbol：委托交易对

```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| page       	| Integer        |   是   |   当前页数    |
| symbol		    	| String   	  	|   否   |   交易对类型，默认所有，可以指定（EOS_ETH）               |
| limit   	| Integer   	    |   否   |   指定获取数据的条数（默认10条，最大500条）            |
| nonce   	| String   	    |   是   |   18位随机数            |
| sign   	| String   	    |   是   |   请求参数的签名            |

　8.POST /market/trade/ticker 查询币种行情（访问频率 10次/2秒）<br>
    URL `https://api.coincax.com/market/trade/ticker`<br>
示例<br>

```
Request
POST　https://api.coincax.com/market/trade/ticker
Response
{
	"code": 0,
	"ticker": {
		"last": 0.00055765,
		"buy": 0.00055752,
		"sell": 0.00055864,
		"high": 0.00058328,
		"low": 0.00055611,
		"vol": 1123610.59,
		"change": -1.67
	},
	"date": 1535878781
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
last：当前价格
buy：买一价格
sell：卖一价格
high：最高价格
low：最低价格
vol：成交量
change：变动
date:当前时间戳

```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| symbol		    	| String   	  	|   是   |   交易对类型，如指定（EOS_ETH）               |

　9.POST /market/trade/kline 查询K线数据（访问频率 10次/2秒）<br>
    URL `https://api.coincax.com/market/trade/kline`<br>
示例<br>

```
Request
POST　https://api.coincax.com/market/trade/kline
Response
{
	"code": 0,
	"kline": [
		[1535846400000, 0.00056745, 0.00056844, 0.00056351, 0.00056464, 36962.90901837],
		[1535850000000, 0.00056472, 0.00056496, 0.00056083, 0.00056273, 61015.48895885],
		...,
	    ...
	],
	"date": 1535879610
}
```
返回值说明
```
code：返回状态，0成功，请参考错误代码
kline:[0]时间戳
      [1]开盘价格
      [2]最高价格
      [3]最低价格
      [4]当前价格
      [5]成交额
date:当前时间戳


```
请求参数

| 参数名	        | 参数类型	    |  必填  | 描述 |
| ------------- |:-------------:| :-----: |:-----:  |
| api_key    	  | String		    |   是   |   用户申请的api_key        |
| symbol		    	| String   	  	|   是   |   交易对类型，如指定（EOS_ETH）               |
| size		    	| Integer   	 |   否  |   指定获取数据的条数  （默认500条，最大500条）              |
| type		    	| String   	 |   否   |   K线时间类型 （1m: 1分钟，1h：1小时，1d：1天，1w：1周，1M：1月）  (默认1d)          |


