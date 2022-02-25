## 一、安装ODL控制器


### 1、安装java


```
apt install openjdk-8-jdk
```


### 2、配置环境


```sh
vim /etc/profile

# 末尾添加
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

source /etc/profile
```


### 3、下载ODL编译好的文件


```
wget https://nexus.opendaylight.org/content/repositories/opendaylight.release/org/opendaylight/integration/karaf/0.8.4/karaf-0.8.4.tar.gz
```


### 4、解压文件


```
tar zvxf karaf-0.8.4.tar.gz
```


### 5、运行


```
cd  karaf-0.8.4
./bin/karaf
```


### 6、常用功能组件


使用 `feature:install` 安装组件。


```sh
# 支持REST API的功能。
odl-restconf

# L2交换机
odl-l2switch-switch

# OpenFlow功能
odl-openflowplugin-drop-test \
odl-openflowplugin-nxm-extensions \
odl-openflowplugin-onf-extensions \
odl-openflowplugin-app-bulk-o-matic \
odl-openflowplugin-app-lldp-speaker \
odl-openflowplugin-app-notifications \
odl-openflowplugin-app-southbound-cli \
odl-openflowplugin-flow-services-rest \
odl-openflowplugin-app-topology-manager \
odl-openflowplugin-app-table-miss-enforcer \
odl-openflowplugin-app-forwardingrules-sync \
odl-openflowplugin-app-topology-lldp-discovery

# 安装DLUX功能
odl-dlux-core \
odl-dluxapps-nodes \
odl-dluxapps-yangman \
odl-dluxapps-yangui \
odl-dluxapps-yangutils \
odl-dluxapps-applications \
odl-dluxapps-yangvisualizer \
odl-mdsal-all
```


以上安装的是较为常用的功能组件，可以根据自己的需求安装，通过 `feature:list` 命令可以列出所有的功能组件，也可以通过 `feature:list -i` 查看已经安装的功能组件。如果要重新安装 `feature`，请`logout`退出，清空安装目录下的data文件夹，再 `./karaf clean`


### 7、登陆 DLUX 界面


访问`IP/index.html`，使用“admin”作为用户名和密码登陆，即可进入主界面。




> 如果登陆异常：可以通过logout退出karaf平台，进入odl主目录，删除data目录，执行./karaf clean，再次重新执行./karaf程序和加载相应组件。



OpenDayLight Web界面中左侧应用导航栏，展示已安装的应用模块，用户可以很直观地查看网络拓扑、主机、流表等信息，通过YANG UI还可以与OpenDaylight进行交互。


### 8、系统配置


有时配置好了Java环境，但是在启动 `Karaf` 时却提示找不到 `JAVA_HOME` ,这是因为 `Karaf` 启动需要Root权限，而之前地Java配置针对地是普通用户，Root用户相关配置还没有设置Java环境。这里提供一种简单的解决方法：在OpenDaylight地/bin目录下找到setenv文件，在文件中加入java环境配置。


```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```
