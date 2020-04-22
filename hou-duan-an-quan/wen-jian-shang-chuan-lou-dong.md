# 文件上传漏洞

### 什么是文件上传漏洞？

用户上传的文件，被当成代码执行。

### 为什么会有文件上传漏洞？

#### 为什么会有文件上传？

* 正常业务需求
* 上传头像，上传报表等

#### 为什么文件上传会造成漏洞？

Web 应用程序的开发模式 1. **File Based** 一个文件对应一个入口点（PHP、ASP） 2. Router Based 一个固定模式的 URL 对应一个函数（Django、Flask、Gin）

### 漏洞触发条件

1. 用户上传文件可被直接访问（例如：在 upload 目录下）
2. 上传的文件会被 web server 解释执行
3. 用户上传的文件内容中恶意的部分不被改变

### 如何防御？

* 前端校验
  * 检查后缀名（[习题](https://buuoj.cn/challenges#[ACTF2020%20%E6%96%B0%E7%94%9F%E8%B5%9B]Upload)）
    * 实现
      * 在浏览器中选择文件，重写 form 的 onsubmit 事件，对文件的信息进行检查
        * 如果符合则 true
        * 不符合则 false 中断文件上传
    * 绕过
      * 修改前端（推荐）
        * 修改 onsubmit 事件
        * 重新定义检查函数
        * 强制提交
      * 构造文件上传包
* 后端校验
  * 检查 MIME
    * 实现
      * 根据前端数据
        * `$_FILE['file']['type'] == 'image/jpeg'`
      * 后端读取文件
        * `$finfo = finfo_open(FILEINFO_MIME);`
        * `$mimetype = finfo_open($finfo, $file_true_name);`
    * 绕过
      * 修改 POST 请求中
  * 检查文件内容是否符合要求（白名单、黑名单）
    * 实现
      * 黑名单

        ![](2020-04-21-05-51-37.png)

      * 白名单？基于文件内容的白名单几乎不可能实现，总有数据的部分，而数据的部分就有机会引入恶意代码。
    * 绕过

      ![](2020-04-21-05-53-14.png)

      ![](2020-04-21-05-55-02.png)
  * 检查后缀名（黑名单）
    * 实现（最经济实惠简单易行）
    * 绕过
      * 支持解析的后缀
        * pht
        * php3
        * php4
        * php5
        * phtml
        * ![](2020-04-21-05-54-03.png)
      * 大小写混合
        * pHp
        * ...
    * 检查后缀名（白名单）
      * 绕过
        * 配合文件包含漏洞
        * 中间件漏洞（如：Nginx 解析漏洞）
  * 检查文件格式
    * 实现
      * getimagesize
    * 绕过
      * 将webshell附加在图片文件后部
* 后端处理
  * 修改文件名（如：时间戳、随机字符串）
    * 绕过
      * 预测随机数
      * 预测服务器时间
  * 隐藏路径
    * 存在问题
      * 如果是用户上传的头像等必须得被访问的数据则不能使用
  * 重新生成文件（如：图片，先读取再生成新的相同像素的图片）
    * 实现
      * 如：createimagefromjpeg、imagecopyresized
    * 绕过
      * [https://secgeek.net/bookfresh-vulnerability/](https://secgeek.net/bookfresh-vulnerability/)
      * [https://blog.safebuff.com/2016/06/17/Bypass-imagecopyresampled-and-imagecopyresized-generate-PHP-Webshell/](https://blog.safebuff.com/2016/06/17/Bypass-imagecopyresampled-and-imagecopyresized-generate-PHP-Webshell/)

### 特殊情况

当 apache 开启 mod rewrite 上传 .htaccess 即可控制解析引擎从而 getshell

