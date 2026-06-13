codex 安装
1. 搞定网络，既然你可访问github,剩下请在github自助查询。
2. 注册一个谷歌账号，或者国外邮箱账号。（谷歌账号允许你用国内邮箱注册，国外邮箱账号请查看chatgpt支持哪种）
3. 使用刚注册的谷歌或者国外邮箱账号注册并登录到chatgpt.
4. 下载codex, 以windows系统为例，先会得到Codex Installer.exe
5. 双击运行Codex Installer.exe会链接到Microsoft Store
6. 如果Microsoft Store 应用提示无法连接网络：(1) 测试能否访问google或者chatgpt，不能就是真的网络有问题；(2)否则，打开UWP回环解锁
7. 下载codex
8. 登录codex 有两种方式：(1) 采用cc-switch中转； (2)使用chatgpt账号登录
9. 采用cc-switch中转，访问[cc-switch仓库](https://github.com/farion1231/cc-switch)，在右侧找到Releases
10. 下载最新版本的cc-switch即可
    
cc-switch的运行逻辑
```
1.在codex客户端发起请求
2.codex读取自身cofig.toml，发现base_url被cc-switch强制修改为http://127.0.0.1:15721/v1,且wire_api锁死为"responses"
codex组装了一个Responses格式的请求体，向本地端口15721发送post请求
3.流量出codex,Windows系统网络层检查该请求的目的地时127.0.0.1
由于在clash 系统代理-排除域名 127.0.0.1，因此系统将该流量与本地直连投递
4.cc-switch在15721端口截获了codex的请求，此时启动内部的入站改写（Inbound Rewrite)机制
4.1路径改写 将v1/responses改写成/v1/chat/completions
4.2数据结构翻译
4.3 模型映射，检查配置的"模型映射表"
5.cc-switch读取自身配置的base_url,发现是"https://router.shengsuanyun.com/api/v1"
然后将请求发给shengsuanyun的服务器
6.shengsuanyun处理请求生成响应，发给cc-switch
7.cc-switch逆向翻译(出站改写),发给codex
8.codex接收并渲染
```

12. 

13. 有两种可迂回方式









