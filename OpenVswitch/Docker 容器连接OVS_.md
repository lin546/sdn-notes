> 本文假设已经安装了 `Open vSwitch`与`Docker`。


## Install ovs-docker utility

正常情况下，安装OVS时默认会安装`ovs-docker`插件，如果没有安装的话，可以通过以下命令进行安装。

```sh
cd /usr/bin
wget https://raw.githubusercontent.com/openvswitch/ovs/master/utilities/ovs-docker
chmod a+rwx ovs-docker
```

## Create an OVS bridge

Here we will be adding a new OVS bridge and configuring it, so that we can get the containers connected on the different network.

```sh
ovs-vsctl add-br ovs-br1
ifconfig ovs-br1 173.16.1.1 netmask 255.255.255.0 up
```

## Add a port from OVS bridge to the Docker Container

- Creat two ubuntu Docker Containers

```
docker run -t -i --name container1 ubuntu /bin/bash
docker run -t -i --name container2 ubuntu /bin/bash
```

- Connect the container to OVS bridge

```
ovs-docker add-port ovs-br1 eth1 container1 --ipaddress=173.16.1.2/24
ovs-docker add-port ovs-br1 eth1 container2 --ipaddress=173.16.1.3/24
```

- Test the connection between two containers connected via OVS bridge using Ping command

## Extra configuration

If the containers are required to be connected to internet then a port is required to be added to the ethernet bridge of host which can be configured as per the command mentioned below. Please add an extra bridge eth1 so that we dont affect the present state of the host.

```sh
ovs-vsctl add-port ovs-br1 eth1
```

## 参考

- [using-ovs-bridge-for-docker-networking](https://developer.ibm.com/recipes/tutorials/using-ovs-bridge-for-docker-networking/)
