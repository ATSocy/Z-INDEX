Thread: znn-qsr-price-feeds
0x3639 | 2024-02-04 11:24:49 UTC | #1

If anyone wants access to a price feeds for:
- ZNN
- QSR
- ETH
- BTC

Please feel free to access them here: https://api.hc1.tools/price

Here is how the results are formatted:
```
{"data":{"btc":{"timestamp":"2024-02-04T11:18:47.640896Z","usd":42982.0},"eth":{"timestamp":"2024-02-04T11:18:47.642709Z","usd":2303.38},"qsr":{"timestamp":"2024-02-04T11:18:47.643184Z","usd":0.138535},"znn":{"timestamp":"2024-02-04T11:18:47.644018Z","usd":1.17}}}
```

This price feed leverages the coincecko free API.  I call this api ever 30 seconds (per the limits of the API). The results are stored in a database and cached for fast access. Users can call the [price API]( https://api.hc1.tools/price) no more than once per second.  If you exceed the rate limit, you will receive this message.   

```
{"code":429,"error":"Too Many Requests"}
```

-------------------------

