title: vps常用性能检测脚本
url: 139.html
id: 139
comments: false
date: 2018-07-14 16:36:52
---
superbench
----------
```bash
wget -qO- git.io/superbench.sh | bash
```

  

memtest测试内存可用量
--------------
```bash
wget https://raw.githubusercontent.com/oooldking/script/master/superbench.sh 
chmod +x superbench.sh 
./superbench.sh
```

  

Zbench
------
```bash
https://raw.githubusercontent.com/FunctionClub/ZBench/master/ZBench-CN.sh && bash ZBench-CN.sh
```

  

Linux性能测试UnixBench一键脚本
----------------------
```bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/unixbench.sh 
chmod +x unixbench.sh 
./unixbench.sh
```

  

94ish版TCP加速脚本
-------------
```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"
chmod +x tcp.sh
./tcp.sh
```

  

SuperSpeed全面测速脚本
----------------
```bash
bash <(curl -Lso- https://git.io/superspeed)
```

  

Yet-Another-Bench-Script
------------------------
```bash
wget -qO- https://raw.githubusercontent.com/masonr/yet-another-bench-script/master/yabs.sh | bash
```

  

Speedtest Monster
-----------------
```bash
curl -LsO bench.monster/speedtest.sh; bash speedtest.sh -Asia
```

Nench
-----
```bash
(curl -s wget.racing/nench.sh | bash; curl -s wget.racing/nench.sh | bash) 2>&1 | tee nench.log
```
