# WiFiT3 0.7.2 for OycZERO

This signed optional package contains the official AArch64 WiFiT3 0.7.2
payload for OycZERO 0010 and later. It includes the applicable GPL notice,
exact upstream provenance and corresponding source archive.

Install it after copying the release asset to DATA:

```sh
oyczero app install /data/wifit3-0.7.2-arm64.oyp
oyczero wifit3
```

A supported external USB wireless adapter is required. OycZERO deliberately
refuses to hand the internal managed `wlan0` interface to WiFiT3. Only audit
networks and equipment that you own or are explicitly authorized to test.
