# https

传输层安全协议（英语：Transport Layer Security，缩写：TLS）。及其前身安全套接层（Secure Sockets Layer，缩写：SSL）是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。

## letsencrypt


#### certbot

[certbot](https://certbot.eff.org/#centosrhel7-nginx) 使用 webroot 的方式进行生成，执行命令

```
# 安装 certbot
yum install certbot

# webroot 验证
certbot certonly --webroot -w /usr/share/nginx/html -d domain.com -m email@email.com --agree-tos

# 更新证书
/usr/bin/certbot renew --quiet --agree-tos

# crontab 定时任务
crontab -e
0 0 1 */1 * /usr/bin/certbot renew --quiet --agree-tos
```

#### acme.sh

安装 [acme.sh](https://acme.sh/)

```
curl  https://get.acme.sh | sh
```

生成证书

```
acme.sh --issue -d mydomain.com --webroot  /usr/share/nginx/html
```

安装证书

```
acme.sh --installcert -d domain.com   \
        --key-file    /etc/nginx/ssl/domain.com \
        --fullchain-file /etc/nginx/ssl/fullchain.cer \
        --reloadcmd  "service nginx force-reload"
```

更新：目前证书在 60 天以后会自动更新

## 参考
[https 配置生成器](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
mozilla https 配置

[crontab.guru](https://crontab.guru/#0_0_1_*/1_*)
crontab 配置图解

[Let's Encrypt 给网站加 HTTPS 完全指南](https://ksmx.me/letsencrypt-ssl-https/)
使用 certbot 给网站 https 的过程，比较详细


## 问题
- openssl 是什么？
- nginx 中的配置项 ssl_trusted_certificate 是什么，怎么配置？



