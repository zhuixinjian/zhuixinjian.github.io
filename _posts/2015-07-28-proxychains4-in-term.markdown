---
layout: post
title: "Proxychains4 proxy in term"
tag: "tags"
---

`gem install jekyll` 毫无反应,而我又用的`ShadowSocks`翻墙,所以网上找了找命令行代理

## proxychains

```
git clone https://github.com/rofl0r/proxychains-ng.git
cd proxychains-ng
./configure
make && make install
cp ./src/proxychains.conf /etc/proxychians.conf
cd .. && rm -rf proxychains-ng

vim /etc/proxychains.conf

socks5  127.0.0.1 1080  //1080改为你自己的端口
proxychains4 wget http://twitter.com

```

齐活!
