## 复制规则高级属性

### 镜像设置 {#-0}

![](/assets/V6.022706.png)

*   “校验方式“：在重镜像（Remirror）过程中有两种校验算法可以选择：时间校验和严格校验。时间校验模式即按照文件的大小以及修改时间来判断文件是否被修改过。严格校验模式则需读取文件的内容做校验。显然时间校验模式速度比严格校验快很多，适合镜像时，工作机端确保无修改操作； 或网络带宽较小且要同步的数据非常大等情形。 对于数据库文件等频繁修改的文件，应该选择 “严格校验”；
*   “错误处理方式“：如果源路径包含系统目录和文件，灾备软件可能无法访问某些特定的系统文件。对于这种情况，软件给出两种解决办法，如下：

1.  在遇到无法访问的文件时，立刻停止镜像；
2.  在遇到无法访问的文件时，记录无法访问的文件后，继续镜像；

*   “文件打开方式“：指在镜像阶段，源端打开文件的方式，该选项只针对Windows工作机有效。在复制阶段，I2是不会读取文件内容的。

1.  “普通文件”：指I2灾备软件以普通文件的方式打开需要镜像的文件，该种方式效率较高；
2.  “MFT”：指I2灾备软件以MFT（Windows OS提供）的方式打开需要镜像的文件，该种方式可以打开已经被其他进程以独占方式打开的文件，比如数据库文件等，该种方式镜像效率相比普通文件方式较差。
3.  “自动选择”：I2灾备软件根据实际情况自动选择打开文件的方式。

*   “文件安全属性”：设置源端的用户权限等安全属性是否同步到备端。
*   “首次镜像方式”：首次镜像方式分为自动和手动方式

1.  “自动”指i2软件拷贝一份完全的数据到灾备机，当需要灾备的数据很大而带宽又不足的时候，完成整个镜像过程可能需要花费很长的时间。
2.  “手工”指在建立复制规则之前，用户已经将数据手动拷贝到灾备机的灾备目录下，i2软件只需要对工作机端的数据和灾备机端的数据进行校验，并拷贝差异部分即可，从而加快镜像的速度。当灾备机为Linux且用卷组保存数据时，必须指定规则的UUID。

### 压缩加密 {#-1}

在数据灾备的过程中，可以定义数据是否要加密，由用户自定义加密的密钥。压缩则可选择三种不同的压缩比，高压缩比可减少数据的传输量，但会消耗一定的资源。

![](/assets/V6.023565.png)

### 快照设置 {#-2}

针对复制规则，用户可自动或者手工生成快照。快照即当前数据的一个“切片”。快照手工生成在复制规则的管理页面中通过手工操作实现。定义快照自动生成的时候，必须定义快照的生成间隔时间、开始时间，以及快照数目参数。当快照达到上限个数是，采用的规则有两种：自动循环或者自动终止。一个快照占用的磁盘空间和当前的数据占用的磁盘空间一样，所以当定义自动快照的时候，要注意有足够的磁盘空间放置相应的快照，不需要的快照通过快照管理及时删除。

![](/assets/V6.023782.png)

### CDP设置 {#cdp}

CDP（Continuous Data Protection，CDP），即持续数据保护。持续数据保护可以捕获或跟踪数据的变化，并将其独立存放在生产数据之外，以确保数据可以恢复到过去的任意时间点。持续数据保护可以为恢复对象提供足够细的恢复粒度，实现任意的恢复时间点。由于CDP记录所有的修改操作以及数据的变化，所以占用的磁盘空间是比较大。I2灾备软件独特的多Baseline支持可以提高配置的灵活性，以及CDP恢复的速度。

通过如下页面设置CDP数据的保存策略：

![](/assets/V6.024021.png)

连续CDP数据的保存天数：指保存连续的CDP数据的天数。

*   按天合并的数据的保留个数：把连续的CDP数据按天合并以减少磁盘占用；
*   CDP处理时间：当连续的CDP数据超过指定的天数后，需要按天合并；如果指定了baseline的生产策略，需要按配置生产Baseline，“CDP处理时间”指定就是这些CDP后台处理的时间。通常，选择业务较为空闲的时间为宜。
*   CDP数据目录：灾备机指定目录下建立文件夹名为该复制规则uuid的目录，存放该复制规则产生的CDP（连续数据保护）数据。要注意的是，因为CDP数据要占用较大的磁盘空间，所以如果用户设置了规则中的CDP属性，则要充分保证该目录的磁盘空间大小。
*   Baseline存储格式：“保持源目录结构”是按Baseline生成时的源端目录结构来存储Baseline；“打包”是将大量小文件打包，目的是缩短恢复时间。
*   创建Baseline副本：创建一个Baseline副本目的也是缩短恢复时间。
*   Baseline（全备份）策略：用户可以指定每周/每月/每年的baseline生成策略。比如，用户如果需要连续CDP数据保存3天；每天生成一个增量备份，增量数据保存一年；CDP生成时间为00:00:00；每周生成一个全备份的数据，全备份数据保存3年；。则可配置如下：

![](/assets/V6.024572.png)

### 孤儿文件 {#-3}

当在某些情况下，某些文件在灾备机端存在，在工作机端不存在时，这些文件被称为孤儿文件。一种可能是灾备机和工作机端的连接由于网络故障或者用户关闭工作机而中断了，在中断的过程中，客户删除了工作机上的某些文件，但这些删除操作导致了灾备通道的中断而没有将相关数据同步到灾备机上，下次恢复灾备的时候，就会发现这些文件只存在于灾备机上。i2灾备软件针对该类型的文件有三种处理方式：

*   不做处理: 即继续保存在灾备机上；
*   删除: 从灾备机上删除掉这些孤儿文件；
*   移动到指定路径: 即将所有的孤儿文件移动到某个特定的目录下统一管理。
    *   归档: 当复制规则处于“复制”状态时，源目录下的某个文件和目录被删除时，目标目录下文件和目录移到指定路径下，实现数据的归档。

![](/assets/V6.024899.png)

### 带宽控制 {#-4}

当在某些情况下，用户想限定带宽的使用，可以通过带宽控制来实现。比如，通过Internet实现数据异地灾备，但同时用户又不想在上班时间影响员工的Internet访问速度，就可以限定工作机时间的带宽。

![](/assets/V6.025005.png)

### 删除复制规则 {#-5}

通过勾选其中一条或多条复制规则，点击删除按钮；或者点击其中一条复制规则的操作栏内的删除图标，删除成功后两端不再同步；

![](/assets/V6.025074.png)

需要注意的是，删除某条复制规则后，灾备端与该复制规则相应的复制数据、CDP数据以及快照数据删除与否，有配置规则的“删除策略”选项决定。