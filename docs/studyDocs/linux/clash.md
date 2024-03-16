# 在linux服务器或笔记本的终端实现翻墙

一、下载clash-core、clash-ui、GeoLite2-Country.mmdb

根据自己电脑的系统和架构进行选择

[clash-core](https://github.com/Kuingsmile/clash-core/releases)

下面两个直接下载

[clash-ui](https://codeload.github.com/haishanh/yacd/zip/refs/heads/gh-pages)

[GeoLite2-Country.mmdb](https://gitee.com/mirrors/Pingtunnel/raw/master/GeoLite2-Country.mmdb)



二、步骤

1. 将GeoLite2-Country.mmdb改名为Country.mmdb 并移动到 ~/.config/clash目录下面
2. 启动clash-core并-f 指定配置文件



三、把梯子设为系统服务

vim /etc/systemd/system/clash.service



```
[Unit]
Description=clash-core
[Service]
Type=simple
ExecStart=/opt/clash/clash-core -f /opt/clash/Huye.yaml
```



刷新服务

systemctl daemon-reload



启动clash服务

systemctl start clash



在~/.bashrc添加

```
#代理
function onproxy() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
    export http_proxy="http://127.0.0.1:7890"
    export https_proxy=$http_proxy
    export all_proxy=socks5://127.0.0.1:7890
    echo -e "\033[32mproxy on!\033[0m"
}

function offproxy(){
    unset http_proxy
    unset https_proxy
    unset all_proxy
    echo -e "\033[31mproxy off!\033[0m"
}
```

source一下



输入onproxy



访问一下google

curl -i google.com

出现返回结果表示翻墙成功



[参考此链接](https://www.youtube.com/watch?v=VOlWdNZAq_o)