# ssh
ssh验证

```
用 GitHub SSH 私钥签名并提交

echo -n 473efc4d30457cf09ee2764ec9ea3ed6 | ssh-keygen -Y sign -n test -f ~/.ssh/<your-key>

GitHub username:
GitHub 用户名: 

SSH Signature:
SSH 签名: 
-----BEGIN SSH SIGNATURE-----
XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
-----END SSH SIGNATURE-----
```
以上是主要html页面，用于验证是否为我的github账号。

其中473efc4d30457cf09ee2764ec9ea3ed6随机生成，每次刷新页面随机刷新

运行之后

~ $ echo -n 473efc4d30457cf09ee2764ec9ea3ed6 | ssh-keygen -Y sign -n lsposed -f ~/.ssh/id_ed25519.pub
Signing data on standard input
-----BEGIN SSH SIGNATURE-----
U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgetrzKOdVHp84kkwNiF8v/Rk4FV
v7jOi3YAPm3Wh8bQYAAAAHbHNwb3NlZAAAAAAAAAAGc2hhNTEyAAAAUwAAAAtzc2gtZWQy
NTUxOQAAAEBdtZKsigTqDsHLASg1lSvYbXkCMbTxSW0roYZbTx1uKSKjVImniLXKnVdhSS
Jcnulj58VjwipQ8H5++vpUWh0H
-----END SSH SIGNATURE-----

这个输出对于473efc4d30457cf09ee2764ec9ea3ed6和 id_ed25519.pub文件相同时， SSH SIGNATURE始终一样

要求输入github用户名 和 ，生成的SSH SIGNATURE
，用于验证是否为我的github账号，
其中github用户名可以通过 https://api.github.com/users/${username}/keys 获取我的 id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDqzj/yAUgIImg5+KrUFWbkfPB9tBqG6BzyXDIM+Kan+xvdPiaUybdTKdztR5Ekk01VUpj3Ojo2ZXfwuTK9LWmlMjJqASJYKUf3lT3G+IAF8uukdLxy0173nQlOfaFQsGlmGpd1ZV5fT8d/19jmKY9Nqf+7yYp4DWERII63qP5tgX/IA6BVEydZqyOs91pvhB9gs/jAxZLSKkZ9fkudxzZgbwCBaC5SkUbvPjDMkQ+8KGVX808oMHoTcNnCqoMzB9bj8XLT/fMudcp7Q0veBqywdcWLo9Vx7I48TnJLw4YXQwJiUSz57BICZHXNzETNMlrXkfLF97MTkkL82OCSw+AsUNpQ1TyYky7xMo++Cn4bme3vWbOZgOaa5a+Gqh8OdrsG5xY2ycmBQ4Orfm0qSLwaOvJs4vThWER6ti6P3iLHOYIynOh+JVC4PTfI71IkqHkZ1AQI+b/Gaw2exP+Knulm1s9sczswnzoIAyYF5fC1+KqLbaD5owWjJIk/RZXPDAU= xxx@xxx.com

这个是在最初运行ssh-keygen之后，把 id_rsa.pub复制到github上去那个

```
https://taoshu.in/git/ssh-sign.html
假设有一个文件/tmp/a.txt，我们想使用~/.ssh/id_ed25519给它做签名，我们可以：

ssh-keygen -Y sign -f ~/.ssh/id_ed25519 -n file /tmp/a.txt
各参数的功能如下：

-Y sign表示计算签名
-f指定私钥
-n file是给签名指定类型
file是我们自己定的，不同类型的签名不会产生冲突
```

ssh-keygen -Y sign -f ~/.ssh/id_ed25519 -n file /tmp/a.txt类似于

echo -n 473efc4d30457cf09ee2764ec9ea3ed6 | ssh-keygen -Y sign -n test -f ~/.ssh/id_ed25519.pub

第一个是输入文件里的文本，第二个是输入文本，-n参数任意
，

ssh-keygen -Y verify -f allowed_signers -I hi@taoshu.in -n file -s /tmp/a.txt.sig < /tmp/a.txt

问题是
/tmp/a.txt.sig 怎么输入文本，(/tmp/a.txt.sig，就是输入 第一个命令生成的-----END SSH SIGNATURE-----），而不是文件
