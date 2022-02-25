OpenvSwitch的操作命令有若干个，其中比较重要的有

- ovs-vsctl：获取或者更改 `ovs-vswitchd` 的配置信息，此工具操作的时候会更新ovsdb-server中的数据库
- ovs-ofctl：操作交换机里的流表
- ovsdb-tool：对ovsdb数据库操作，不经过ovsdb-server模块

## 一、ovs-vsctl

前面已经介绍过了ovs-ovsctl命令是对交换机上网桥和端口等信息进行配置的命令。这里首先需要说明一下ovs的概念中 ‘桥’ 这个词的意思就是指交换机。我们说创建一个网桥，其实说的意思就是创建一个交换机。而端口则是指交换机的网口。

**常用命令**：

| 命令 | 含义 |
| --- | --- |
| init | 初始化数据库（前提是数据分组为空） |
| show | 打印数据库信息概要 |
| emer-reset | 将OVS配置复位为空状态 |
| add-br BRIDGE | 添加新的网桥 |
| del-br BRIDGE | 删除网桥 |
| list-br | 打印网桥摘要信息 |
| list-ports BRIDGE | 打印网桥中所有端口摘要信息 |
| add-port BRIDGE PORT | 向网桥中添加端口 |
| del-port [BRIDGE] PORT | 删除网桥上的端口 |
| get-controller BRIDGE | 获取网桥的控制器信息 |
| del-controller BRIDGE | 删除网桥的控制器信息 |
| set-controller BRIDGE TARGET.. | 向网桥添加控制器 |


## 二、ovs-ofctl

该工具是OpenFlow交换机的命令行管理工具，用于管理OVS作为OpenFlow交换机时的各种参数，用户可以通过ovs-ofctl查询或修改 `OpenFlow` 交换机的状态、配置和流表项等信息。ovs-ofctl命令格式为ovs-ofctl[命令][选项],常用命令见表：

| 命令 | 含义 |
| --- | --- |
| show switch | 输出Openflow信息 |
| dump-ports SWITCH [PORT] | 输出端口信息 |
| dump-ports-desc SWITCH | 输出端口描述信息 |
| dump-flows SWITCH | 输出交换机中所有的流表项 |
| dump-flows SWITCH FLOW | 输出交换机中匹配的流表项 |
| add-flow SWITCH FLOW | 向交换机添加流表项 |
| add-flows SWITCH FILE | 从文件中向交换机添加流表项 |
| mod-flows SWITCH FLOW | 修改交换机的流表项 |
| del-flows SWITCH [FLOW] | 删除交换机的流表项 |


说明：若需要设置允许的OpenFlow版本(默认为v1.0)可以使用选项`-O`或`--protocols`进行设置；若需要查看命令的帮助信息，可以使用选项`-h`或`--help`进行查看；若需要查看版本信息，可以使用选项`-v`或`--version`进行查看。
