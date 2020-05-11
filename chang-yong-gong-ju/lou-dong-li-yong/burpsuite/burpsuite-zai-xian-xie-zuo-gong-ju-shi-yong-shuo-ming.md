# BurpSuite 在线协作工具使用说明

好消息！好消息！Web 狗的福音来辣！

* 你是否还在为没有趁手的 BurpSuite 协作插件而烦恼？
* 你是否还在为如何给队友共享 BurpSuite 中辛辛苦苦调教好的请求？
* 你是否还在用最原始的 Copy to File 然后通过 QQ 发送给队友来共享 BurpSuite 的请求？

BurpSuite-Team-Extension 是一款可以解放 Web 狗双手的插件！有了它你可以一键为你的队友分享资（Req）源（uest）！快来试试吧！

### 前置需求

1. BurpSuite Professional

### 安装

1. 运行 BurpSuite
2. Extender-&gt;Extension-&gt;Add

    ![](figure/01.png)

3. 选择 `BurpSuite-Team-Extension/target/BurpSuiteCollaborationClient.jar`

    ![](figure/02.png)

4. 此时 BurpSuite 主标签将会出现 Burp TC，表示安装成功

### 配置

1. 进入 Burp TC，填入如下配置

   | Key | Value |
   | :---: | :---: |
   | Display Name |  |
   | Server Address |  |
   | Server Port |  |
   | Server Password |  |

2. 选择下方 Configuration 标签
3. 配置 “Select Certificate” 为 burpServer.pem
4. 配置 “Select Certificate Key” 为 burpServer.key
5. 点击 “Connect” 按钮
6. 成功连接之后如下图

    ![](figure/03.png)

   **协作**

#### 房间

**创建房间**

1. 点击 “New Room” 按钮
2. 输入房间名称与密码

    ![](figure/04.png)

3. 房主默认进入房间，在右侧区域可以看到聊天室中的成员

**加入房间**

1. 连接成功后
2. 右侧区域则变成当前服务器的房间列表
3. 选择想要加入的房间，右键 -&gt; Join
4. 输入对应密码即可加入

**离开房间**

1. 点击 “Leave Room”
2. 右侧区域则变成当前服务器的房间列表

#### 分享 Request

1. 加入房间
2. 选择你想要分享的请求，如：在 Repeater 中有一条请求你想要分享
3. 在 Repeater 的对应请求内容空白处点击右键 -&gt; Share Repeater Payload

    ![](figure/05.png)

4. 可以选择分享给整个 Group，也可以选择分享给单独的人

#### 创建短链接（暂时不好使）

1. 选择你想要分享的请求
2. 右键 -&gt; CreateLink

### 参考链接

* [BurpSuite-Team-Extension](https://github.com/Static-Flow/BurpSuite-Team-Extension/)
* [演示视频](https://www.youtube.com/watch?v=eXlT3cTOL-4)

