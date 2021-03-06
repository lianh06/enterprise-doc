## 恢复虚机

### 恢复原虚机 {#-0}

在控制机管理界面，通过 虚拟机支持-&gt;虚拟平台恢复，来添加/编辑恢复规则，恢复规则添加/编辑页面如下：

![说明: 1](/assets/V6.037082.png)

*   “任务名称”：客户命名的名称，便于管理；
*   “灾备机”：储存备份数据的备机；
*   “数据存放目录”：选择备份数据储存的路径；
*   “选择备份点信息”：备份数据的备份时间及大小；

### 新建虚机 {#-1}

在控制机管理界面，通过 虚拟机支持-&gt;虚拟平台恢复-&gt;高级设置-&gt;勾选创建新的虚机，来添加/编辑恢复新建虚机的规则，规则添加/编辑页面如下：

![说明: 1](/assets/V6.037244.png)

*   “虚拟机”：客户命名的名称，方便管理；
*   “恢复目标虚拟平台”：选择恢复的虚拟平台；
*   “数据中心”：虚拟平台数据中心；
*   “主机名称”：所选虚拟平台的主机名称；
*   “数据存储”：虚拟平台上的数据存储磁盘；
*   “虚拟机磁盘列表”：在基本设置中选择完备份时间点后，虚拟机磁盘列表显示相对应的虚拟机磁盘；
*   “处理器数量”：根据客户需求设定处理器数量；
*   “处理器的核心数量”：根据客户需求设定处理器的核心数量；
*   “内存”：根据客户需求设定内存大小；
*   “MAC地址”：需要在页面上删除MAC地址，虚机在创建时会分配新的MAC地址，删除后，页面显示如下：

![说明: 1](/assets/V6.037514.png)

**注意：**

恢复任务完成后，虚拟平台上相对应的虚机处于开启状态。

### 恢复规则列表 {#-2}

添加恢复任务，页面如下：

![说明: 1](/assets/V6.037568.png)

恢复规则包含如下状态：

*   “准备中”：准备恢复；
*   “已恢复”：正在恢复；
*   “完成”：恢复已完成；

针对恢复规则可用的操作，从左到右如下：

*   “启动”：启动规则；
*   “停止”：停止规则；
*   “修改”：修改规则；
*   “删除”：修改规则；
*   “查看日志”：查看任务日志；