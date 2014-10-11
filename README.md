nginx-reverse-proxy-to-google-with-ssl
======================================

+ 请将 g.foo.bar 替换为你反向代理的 google 的域名
+ 请将 /var/nginx/cache/one 替换为你的nginx缓存目录，max_size为缓存区大小，需要对应的权限设置；
+ upstream google 段是设置的 google 原始可正常访问的 IP 的负载均衡，可以在自己的服务器上 ping 一下 google，找到快的 IP；
+ 反向代理中考虑到自动关键字提示，替换了对应的 cookie，如果被 google block，请尝试更换该 cookie 内容；
+ 443 端口需要替换对应的证书，当然你用自己签发的也没关系，建议使用免费的 ssl 证书。

额外注意
--------------------------------------
> nginx 启用了设置了密码的证书的 ssl 之后，每次 restart 或者 reload 需要输入证书的密码(类似于提示：Enter PEM pass phrase:)。
> 如果你觉得烦，解决方法如下：
openssl rsa -in 你的ssl密钥.key -out 你的ssl密钥.key.unsecure
然后将配置中的 ssl_certificate_key 你的 ssl 密钥.key; 更改为 ssl_certificate_key 你的 ssl 密钥.key.unsecure;
