## 节点管理

I2软件从6.0版本开始使用节点的方式管理，不在凸显工作机灾备机的模块，节点添加的方式分为3种类型，工作机，灾备机和混合节点，如果一个节点作为混合节点时，则它可以作为工作机也可以作为灾备机，另外要说明的是，只有混合节点才能作为HA规则的节点。

如下介绍节点添加过程：

![](/assets/V6.016151.png)

点击“新建”按钮，进入如下的节点新建页面。在此输入相关的工作机信息：

![](/assets/V6.016188.png)

*   “名称“：客户命名的节点名称，便于管理
*   “管理接口地址”: 管理接口地址就是节点用于和控制机通讯的IP地址。如果工作机有多个网卡，用户可以配置管理和数据走不同的网卡。
*   “管理接口端口”：管理接口端口就是节点用于和控制机通讯的端口（默认是26821），可在etc目录下i2port.conf查询；Windows路径是&lt;安装路径&gt;\etc\i2port.conf；Linux路径是/etc/sdata/i2port.conf；
*   “数据接口地址”： 即工作机用于和灾备机进行通讯和数据传输的地址。
*   “账号“：对应工作机操作系统的登录账号。i2软件支持域用户验证，Windows域用户名格式为：&lt;Domain Name&gt;\&lt;User Name&gt;
*   “口令“：对应工作机操作系统的登录口令。
*   “节点类型”: 节点类型分为3类: 工作机、灾备机、混合主机

    工作机（Source Server）：是指客户的生产机，I2软件安装在工作机来镜像和同步数据到灾备机

    灾备机（Target Server）：是指客户用于备份的机器，用来接收来自工作机发送过来的数据。

    混合节点：混合节点可以作为工作机也可以作为灾备机，作为HA的节点时，添加的节点类型必须为混合节点。

*   “软件许可“：不同的license可以管理不同的节点类型，可复选，由于功能时通过license管理的，所以选择的注册的节点，响应的license未选择时，功能不可复用。
*   “日志目录”：灾备软件自身产生的日志所存放的目录

![](/assets/V6.016822.png)

*   “数据缓存目录”：数据缓存目录为放置要灾备数据的磁盘缓冲区，一般情况下，数据直接从灾备内存中直接取出并灾备到远端，但在某些异常情况下，如网络异常、带宽不足、远端灾备系统异常、灾备巨大文件等，导致数据不能及时灾备到远端，此时在一定时间范围内，将部分数据从灾备内存中缓冲到磁盘上。保证系统在窄带、大文件等环境下都能正常运行。
*   “内存使用上限“：分配给灾备软件用于数据缓存所能使用的内存上限。
*   “磁盘使用上限“：分配给灾备软件用于数据缓存所能使用的磁盘上限。注意，如果该值设置为0，表示不进行磁盘缓存，一旦变化的数据超过内存缓存大小，复制规则将自动停止，从而最大限度地保护工作机资源。复制规则停止后，管理员需要手动启动复制规则才能重新进行数据保护。
*   “复制路径”: 要灾备的数据所属的路径。如工作机为linux系统，则需在此指定源路径；如工作机为windows系统，不需要指定复制路径，在后面创建复制规则时用户自行选择路径，且复制路径可多选。

    注意事项：

    注册linux工作机、混合节点时，必须确保“复制路径”包含要监控的文件系统操作所涉及的对象。

    比如rename操作的情形，要包含rename的源和目标。通常把“复制路径”设置为根目录&quot;/&quot;。

![](/assets/V6.017348.png)

*   “灾备机设置“：如果支持快照选中快照支持（linux 有此选项）
*   “快照支持”：无需快照功能不用勾选此项；指定该Linux灾备机是否支持快照。如果该灾备机需要支持级联灾备方式，则不能勾选该选项；比如有A、B、C三台机器，如果想把A机数据灾备到B机，B机再把从A备份来的数据灾备到C机，那么B机即是灾备机又是工作机，不能勾选“快照支持”选项。
*   “卷组（VG）名称“：对于支持快照的Linux灾备机，i2软件采用卷组存放复制和快照数据，因此必须指定卷组。 表格中列出了该灾备机上所有的卷组，从中选择一个作为i2灾备软件使用。当该灾备机不需要支持快照，则不需要指定卷组。

如果用户想查看系统状态，在添加节点时需打开监控设置

![](/assets/V6.017659.png)

*   “监控延迟“：节点发送信息到控制机时间间隔
*   “分析数据目录”：节点监控信息保存日志目录，日志信息一天生成一个文件
*   “监控数据保留“：控制机数据库保存数据天数
*   “分析数据保留“：分析数据日志保存天数，

提交之后，会看到如下的节点列表窗口中出现刚创建的节点信息:

![](/assets/V6.017793.png)

如果节点模块工作正常，且控制机和节点通讯正常的话，节点的状态会显示为“在线”状态，i2灾备软件会定时刷新该状态信息，其对应的操作有四种，从左到右依次为：“修改”，“删除”，“查看磁盘空间”，“查看日志”，“系统状态”。只有在该节点没有被任何复制规则使用的时候，才能被修改或删除。