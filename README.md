### It is recommended that you read the official document first

Coinex spot docs [https://github.com/coinexcom/coinex_exchange_api/wiki](https://github.com/coinexcom/coinex_exchange_api/wiki)

Coinex futures docs [https://github.com/coinexcom/coinex_perpetual_api](https://github.com/coinexcom/coinex_perpetual_api)

All interface methods are initialized the same as those provided by Coinex. See details [src/api](https://github.com/zhouaini528/coinex-php/tree/master/src/Api)

Most of the interface is now complete, and the user can continue to extend it based on my design, working with me to improve it.

[中文文档](https://github.com/zhouaini528/coinex-php/blob/master/README_CN.md)

### Other exchanges API

[Exchanges](https://github.com/zhouaini528/exchanges-php) It includes all of the following exchanges and is highly recommended.

[Bitmex](https://github.com/zhouaini528/bitmex-php) Support [Websocket](https://github.com/zhouaini528/bitmex-php/blob/master/README.md#Websocket)

[Okex](https://github.com/zhouaini528/okex-php) Support [Websocket](https://github.com/zhouaini528/okex-php/blob/master/README.md#Websocket)

[Huobi](https://github.com/zhouaini528/huobi-php) Support [Websocket](https://github.com/zhouaini528/huobi-php/blob/master/README.md#Websocket)

[Binance](https://github.com/zhouaini528/binance-php) Support [Websocket](https://github.com/zhouaini528/binance-php/blob/master/README.md#Websocket)

[Kucoin](https://github.com/zhouaini528/kucoin-php)

[Mxc](https://github.com/zhouaini528/Mxc-php)

[Coinbase](https://github.com/zhouaini528/coinbase-php)

[ZB](https://github.com/zhouaini528/zb-php)

[Bitfinex](https://github.com/zhouaini528/bitfinex-php)

[Bittrex](https://github.com/zhouaini528/bittrex-php)

[Kraken](https://github.com/zhouaini528/kraken-php)

[Gate](https://github.com/zhouaini528/gate-php)   

[Bigone](https://github.com/zhouaini528/bigone-php)   

[Crex24](https://github.com/zhouaini528/crex24-php)   

[Bybit](https://github.com/zhouaini528/bybit-php)  

[Coinbene](https://github.com/zhouaini528/coinbene-php)   

[Bitget](https://github.com/zhouaini528/bitget-php)   

[Poloniex](https://github.com/zhouaini528/poloniex-php)

[Coinex](https://github.com/zhouaini528/coinex-php)

**If you don't find the exchange SDK you want, you can tell me and I'll join them.**

#### Installation
```
composer require linwj/coinex
```

Support for more request Settings
```php
$coinex=new CoinbeneSpot();

//You can set special needs
$coinex->setOptions([
    //Set the request timeout to 60 seconds by default
    'timeout'=>10,
    
    //https://github.com/guzzle/guzzle
    'proxy'=>[],

    //https://www.php.net/manual/en/book.curl.php
    'curl'=>[],
]);
```

### Exchange Spot

Market API [More](https://github.com/zhouaini528/coinex-php/blob/master/tests/exchange/market.php)

```php
$conex=new CoinexExchange();

try {
    $result=$conex->market()->getMarketList();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$conex->market()->getMarketTicker([
        'market'=>'BCHBTC'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$conex->market()->getMarketDepth([
        'market'=>'BCHBTC',
        'merge'=>'0.1'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$conex->market()->getMarketKline([
        'market'=>'BCHBTC',
        'type'=>'4hour'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```

Account API [More](https://github.com/zhouaini528/coinex-php/blob/master/tests/exchange/account.php)

```php
$conex=new CoinexExchange($key,$secret);

try {
    $result=$conex->account()->getBalanceInfo([
        //You can 'access_id' and 'tonxe' leave it blank
        'access_id'=>$key,
        'tonce'=>time().'000',
    ]);

    //You can 'access_id' and 'tonxe' leave it blank
    $result=$conex->account()->getBalanceInfo();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    //You can 'access_id' and 'tonxe' leave it blank
    $result=$conex->account()->getBalanceCoinWithdraw();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$conex->account()->getCreditInfo();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```


Trading API [More](https://github.com/zhouaini528/coinex-php/blob/master/tests/exchange/trading.php)

```php
$conex=new CoinexExchange($key,$secret);

try {
    //You can 'access_id' and 'tonxe' leave it blank
    $result=$conex->trading()->postMarket([
        //'access_id'=>'xxxxx',
        //'tonce'=>time().'000',
        'market'=>'BCHBTC',
        'type'=>'sell',
        'amount'=>'1',
        'client_id'=>'99999999',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    //You can 'access_id' and 'tonxe' leave it blank
    $result=$conex->trading()->getStatus([
        //'access_id'=>'xxxxx',
        //'tonce'=>time().'000',
        'id'=>'99999999',
        'market'=>'BCHBTC',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    //You can 'access_id' and 'tonxe' leave it blank
    $result=$conex->trading()->deletePending([
        'id'=>'9999999',
        'market'=>'BCHBTC',
        'type'=>'0'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```


Margin API [More](https://github.com/zhouaini528/coinex-php/blob/master/tests/exchange/margin.php)

```php
$conex=new CoinexExchange($key,$secret);

try {
    //You can 'access_id' and 'tonxe' leave it blank
    $result=$conex->margin()->getAccount([
        'market'=>'BCHBTC'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$conex->margin()->getMarket();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```

More Test [more](https://github.com/zhouaini528/coinex-php/blob/master/tests/exchange)

### Perpetual Futures






