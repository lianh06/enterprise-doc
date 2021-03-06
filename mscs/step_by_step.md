## 详细步骤

### 安装i2软件 {#i2}

请按照“安装和卸载”一章的说明，安装i2软件。

### 创建i2资源类型 {#i2-0}

选择任何一个Cluster Node，进入C:\WINDOWS\cluster，编辑i2mscs.bat文件，请将第二行前的：号去掉（第一次安装时默认已去，因此不用编辑直接双击即可），见下图，然后双击i2mscs.bat文件

然后打开cmd，输入命令“cluster resourcetype”确认i2资源类型已创建，见下图，可以看到资源类型名为“Info2Soft Connection Resource”，说明创建成功。资源创建只需在任意一个Node上完成即可。

在Windows 2008上，创建i2资源类型的步骤和Windows2003相同。

### 添加i2资源实例 {#i2-1}

Windows 2003系统中添加i2资源实例的详细步骤如下：

在群集应用组中右键点击新建-&gt;资源，见下图，资源类型选择“Info2Soft Connection Resource”，组选择群集应用所在的组，点击下一步

将所有节点添加到“可能的所有者”，点击下一步

将应用对外IP地址和共享磁盘添加到该资源依存，注意这一步是必须的，否则会无法在控制机上创建集群，点击完成

创建成功后该资源默认脱机，右键资源点击“联机”，至此i2资源实例添加完成。

在Windows2008系统上，创建的步骤类似，所不同的是在创建i2资源后，需要右键点击i2资源实例编辑属性，选择依赖的IP和共享磁盘。详细步骤如下：

打开故障转移群集管理窗口，在用户创建的应用程序实例如SQL2008中，右边操作栏点击“添加资源”-&gt;”更多资源”，点击“Info2Soft Connection Resource”，在摘要栏出现“新建Info2Soft Connection Resource”实例

右键点击该资源实例属性，更改资源名称（任意），见下图：

点击“依赖关系”标题栏，插入应用对外IP地址以及共享磁盘（与关系），然后确定，见下图：

右键该资源点击“使该资源联机”，效果见下图，至此添加i2资源实例完成。

### 配置集群应用 {#-0}

打开控制机界面，进入集群管理--&gt;集群管理，点击“新建”

*   “名称“：用户自己定义的在i2控制机上的集群应用的名字；
*   “集群类型“：目前i2支持Windows集群，更多集群类型后续开发中；
*   “i2应用IP地址“：i2资源实例所依赖的IP地址，比如在如上的配置中，就是i2soft所依赖的IP地址；

“非Cluster本身的地址”：若不勾选，填的ip必须是i2资源依赖的那个ip；若勾选了，应用ip地址可以指定任意的ip地址

*   “管理接口端口“：管理接口端口就是工作机用于和控制机通讯的端口（默认是26821），可在etc目录下i2port.conf查询；Windows路径是&lt;安装路径&gt;\etc\i2port.conf；Linux路径是/etc/sdata/i2port.conf；
*   “域用户名“：Cluster所指定的域用户名；
*   “口令”：域用户名对应的密码；
*   “集群名”：Cluster Name，控制机自动获取；
*   “共享磁盘”：选择i2资源实例所依赖的共享磁盘盘符；
*   “集群节点”：i2软件要求每个Cluster 节点注册为工作机；控制机会自动将Cluster节点对应到工作机。如果Cluster节点没有注册，可以点击“新建”链接创建；当工作机新建完成后，工作机验证会页面会显示“验证成功”，见下图，然后提交

集群应用列表见下图：

### 为集群应用创建复制规则 {#-1}

控制机界面：进入集群管理-&gt;复制规则，点击“新建”，见下图：

创建集群的复制规则流程与普通的复制规则差不多，区别在于这里只能选择集群管理已创建的集群，“灾备机目标路径”选择灾备机的存放目录，提交后即开始镜像-复制，效果见下图：