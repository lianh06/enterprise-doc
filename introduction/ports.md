## 端口说明

| 服务器角色 | 端口 | 协议 | 监听端口 | 注备 |
| --- | --- | --- | --- | --- |
| 工作机 | RPC服务端口 | TCP | 26821 | 控制机-&gt;工作机 |
|  | HA服务端口 | UDP | 26860 | 工作机-灾备机，用于高可用功能相关 |
| 灾备机 | RPC服务端口 | TCP | 26821 | 控制机-&gt;灾备机 |
|  | 镜像端口 | TCP | 26832 | 工作机-&gt;灾备机 |
|  | 复制端口 | TCP | 26833 | 工作机-&gt;灾备机 |
|  | 恢复端口 | TCP | 26831 | 工作机-&gt;灾备机 |
|  | HA服务端口 | UDP | 26860 | 工作机-灾备机，用于高可用功能相关 |
| 控制机 | HTTP端口 | TCP | 58080 | HTTP端口 |
|  | HTTPS端口 | TCP | 55443 | HTTPS端口 |