# MAC



## 刷新 DNS  缓存



````````bash
 # 刷新 DNS Cache
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder; say DNS cache flushed
````````

