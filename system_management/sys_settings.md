## 系统参数

### 全局参数设置 {#-0}

![](/assets/V6.018903.png)

*   “控制机地址”：这个地址不一定是控制机本身的地址，节点通过“控制机地址”来访问控制机。
*   “页面刷新时间”：有些页面需要实时监控状态，“页面刷新时间”配置多久更新一次状态。在网络状况不佳的情况下，这里可以选择大一点的间隔时间，如果网络状况很好，可以用默认的间隔时间。
*   “每页显示记录数”：每页显示的记录条数。
*   “控制机超时时间”：设置控制机超时时间（未进行任何操作）
*   “日志保存时间”：节点/复制规则的保存时间，旧的日志将被删除，防止控制机数据库记录过多而影响访问速度。
*   “邮件语言”：控制机发送邮件通知时，采用的语言；

**特别说明：**

“页面刷新时间”和“每页显示记录数”这两个参数配置后，必须重新登录才会生效。

### 安全相关设置 {#-1}

![](/assets/V6.019219.png)

*   “会话并发数”：同时在线的用户（普通管理员，普通用户，查看用户等）数量。
*   “允许尝试登陆次数”：登陆时如果用户名和密码输错的次数大于设置的参数，页面就会锁定，提示15分钟之后再次登陆。
*   是否开启验证码：页面登陆时如果此选择“是”会有输入验证码的这一项。
*   限制密码复杂度：此选项如果选择“是”创建用户或修改密码时会做用户密码复杂度检测，密码太简单不给注册。

### 监控提醒通知设置 {#-2}

![](/assets/V6.019408.png)

*   “Email通知”：启用邮件通知服务。
*   “SMTP的服务器地址”：SMTP的服务器地址。
*   “使用SSL连接服务器”：是否使用SSL连接服务器；需要注意和SMTP服务器端口的配合。
*   “SMTP的服务器端口”：通常非SSL连接和SSL连接的端口是不同的。
*   “邮箱帐号”：发送邮件的帐号。
*   “邮箱密码”：当用该帐号发送邮件时，SMTP服务器需要做认证。该密码用于SMTP服务器认证。
*   “监控对象”：状态：监控工作机/灾备机/复制规则/高可用规则，如果发现状态异常，发送Email到用户指定的邮箱。
*   “连续通知次数”：连续发送Email的次数，如果控制机发现状态异常，控制机连续发送Email的次数，防止把用户的Email信箱被塞满。
*   “保存”：保存本页的配置信息。
*   “重置用户连续通知”：当Email发送次数达到连续发送的上限之后，控制机就不再继续发送Email，点击该按钮，可以使控制机继续发送Email到用户指定的邮箱。
*   “发送测试Email”: 利用该页面的SMTP设置，发送测试Email到当前登录用户的邮箱。当前登录用户的邮箱设置通过用户管理修改。
*   “接收提醒的Email”：发送测试邮件时，接收的邮箱。