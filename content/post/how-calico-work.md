---
title: "How does calico work with kubernetes"
date: 2018-02-14T19:00:00+08:00
tags:
- kubernetes
archives:
- kubernetes
categories:
- kubernetes
coverImage: "https://res.cloudinary.com/ddvxfzzbe/image/upload/v1513355392/ChMkJ1f8ljWIBAmcAA-gWT6p-0oAAWzegGSHVwAD6Bx012_telyks.jpg"
thumbnailImage: https://res.cloudinary.com/ddvxfzzbe/image/upload/v1542166411/uuopzhfeswhmr1tptrs4.jpg
---

了解calico作为kubernetes的cni插件是如何工做的。
<!--more-->

在解决容器网络的问题上,docker和kubernetes分别提出了CNM和CNI两个标准.但是kubernetes逐渐成为容器集群方案首选的时候,作为使用者,我们不得不去调研和测试开源的cni-plugin来解决我们容器环境的网络问题.cluster network addons来解决集群里网络互联互通的问题.kubernetes在[kubernetes networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/) 明确提出对CNI插件实现的要求：

1. all containers can communicate with all other containers without NAT
2. all nodes can communicate with all containers (and vice-versa) without NAT
3. the IP that a container sees itself as is the same IP that others see it as

官网列出了很多实践,除了云平台提供的实现外,比较活跃的项目有calico,flannel,weave.每个project各有优点我们来看一个早期的对比文章[calico-flannel-weave](http://chunqi.li/2015/11/15/Battlefield-Calico-Flannel-Weave-and-Docker-Overlay-Network/).除此之外，还建议看看docker官方CNM的文档[docker-CNM](https://success.docker.com/article/networking)
对比理解.

# Calico
Calico为容器网络提供了一个layer3的实现方式,packets在容器之间不需要封装和NAT.

calico arch:
![calico arch](https://res.cloudinary.com/ddvxfzzbe/image/upload/v1543404693/calico-arch-gen-v3.2_t04nry.svg)


要看的几篇文章：
## 安装
>   推荐参考kubernetes和calico的文档，不多赘述.

[install calico on kubernetes](https://docs.projectcalico.org/v3.3/getting-started/kubernetes/installation/calico)

## calico的工作原理:
>   flannel is a virtual network that gives a subnet to each host for use with container runtimes.

### node-to-node mesh

### IPIP

### BGP Route Reflector

参考：

https://docs.projectcalico.org/v3.1/reference/architecture/
https://docs.projectcalico.org/v3.1/reference/architecture/components
https://docs.projectcalico.org/v3.1/reference/architecture/data-path
https://docs.projectcalico.org/v3.1/reference/private-cloud/l2-interconnect-fabric
https://docs.projectcalico.org/v3.1/reference/private-cloud/l3-interconnect-fabric
