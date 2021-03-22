.. _sre-structure:

*********
架构
*********


* 双云架构
* 大数据监控
* 微服务架构

双云架构
========


所谓双云就是主机群在一个数据中心，备集群在另一个数据中心，正常的流量走向是全部到主集群，如果一个数据中心出现问题，会自动切换到备集群，以实现主备架构，保证业务不会中断。

名词解释
--------------

域名
    一个网站的的入口、名字。

ELB
    Elastic Load Balancer, 弹性负载均衡，让ELB后端的服务能平衡地承接用户访问的流量，主要是流量的转发。

SLB
    Software Load Balancer，软件负载均衡，使用openresty实现，openresty由nginx和lua脚本组成，主要是根据uri转发流量到不同机房、限流、灰度规则设置等等。

一般架构是域名到两个ELB，两个ELB转发流量到相同的几台SLB服务器，最后由SLB转发到具体的微服务服务器，微服务有3个集群，分别是主、备集群和灰度集群，以形成双云的结构。

架构图
--------------

.. blockdiag::


    blockdiag double-cloud {

        orientation = portrait

        A [ label = "域名", shape = cloud];
        B [ label = "主ELB的公网IP", shape = roundedbox];
        C [ label = "备ELB的公网IP", shape = roundedbox];
        D [ label = "同样的SLB服务器"];
        E [ label = "同样的SLB服务器"];
        G [ label = "服务器，微服务现网主集群，部署在主机房", stacked];
        F [ label = "微服务灰度集群", stacked];
        H [ label = "微服务现网备集群，部署在备机房", stacked];

        A -> B;
        A -> C;
        B -> D;
        C -> E;
        D -> G [ label = "主" ];
        E -> G;
        D -> F [ style = dashed , label = "灰度"];
        D -> H [ style = dashed , label = "备"];

        group elb {
        B; C;
        label = "E L B";
        fontsize = 16;

        color = "orange";
        style = dashed;
        shape = line;
        }

        group slb {
        D; E;
        label = "S L B";
        fontsize = 16;
        color = "lightgreen";
        style = dashed;
        shape = line;

        }


   }


域名到ELB，比如 idlepig.cn 这个域名后端配置两个A记录，分别对应的是两个ELB的公网IP，端口是443端口，对应的协议是https，证书也是绑定在ELB上面，这样用户访问域名的时候，流量会转发到两个IP上面。

ELB到SLB，两个ELB的分别绑定同样的SLB服务器，SLB的端口是8080，这样域名到ELB的443端口，再把流量转发到SLB的8080端口。

SLB到后端服务器，SLB由openresty搭建，openresty由nginx加lua脚本，扩展了nginx的功能。SLB通过不同的uri把不同的流量转发到不同的后端集群，比如平时流量都是到主集群，灰度变更的时候，通过配置规则，可以让流量转发到灰度集群，当主集群出现问题的时候，流量会自动转发到备集群。

.. _sre-structure-todo-slb-config:

todo, 具体的SLB配置
----------------------


具体配置：上面描述对应的结构图
---------------------------------------

.. blockdiag::

   blockdiag double-cloud-ip {

        orientation = portrait


        A [ label = "https://www.idlepig.cn", shape = cloud, width = 220];
        B [ label = "49.4.1.2:443", shape = roundedbox];
        C [ label = "49.4.1.3:443", shape = roundedbox];
        D [ label = "10.3.1.2:8080;\n10.3.1.3:8080;\n10.3.1.4:8080;\n10.3.1.5:8080", height = 60];
        E [ label = "10.3.1.2:8080;\n10.3.1.3:8080;\n10.3.1.4:8080;\n10.3.1.5:8080", height = 60];
        G [ label = "10.6.49.9:18080;\n10.6.49.10:18080;\n10.6.49.11:18080", stacked];
        F [ label = "10.5.23.7:18080;\n10.5.23.8:18080", stacked];
        H [ label = "10.7.49.9:18080;\n10.7.49.10:18080;\n10.7.49.11:18080", stacked];

        A -> B;
        A -> C;
        B -> D;
        C -> E;
        D -> G [ label = "主" ];
        E -> G;
        D -> F [ style = dashed , label = "灰度"];
        D -> H [ style = dashed , label = "备"];

        group elb {
        B; C;
        label = "E L B";
        fontsize = 16;
        color = "orange";
        style = dashed;
        shape = line;
        }

        group slb {
        D; E;
        label = "S L B";
        fontsize = 16;
        color = "lightgreen";
        style = dashed;
        shape = line;

        }

   }



大数据监控
============


业务服务器 - flume - 流kafka - spark - 批kafka - es - kibana

业务服务器 - flume - 流kafka - spark - 批kafka - druid - 前端报表

自动化运维平台-模块
==================


.. mdinclude:: structure_ops_system.md

.. mdinclude:: add_hosts.md