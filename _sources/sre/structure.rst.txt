.. _sre-structure:

*********
架构
*********


* 双云架构
* 大数据监控
* 微服务架构

双云架构
========

**文字说明**

.. blockdiag::


    blockdiag double-cloud {

        orientation = portrait

        A [ label = "域名", shape = cloud];
        B [ label = "主ELB的公网IP", shape = roundedbox];
        C [ label = "备ELB的公网IP", shape = roundedbox];
        D [ label = "几台同样的SLB机器"];
        E [ label = "几台同样的SLB机器"];
        G [ label = "微服务现网主集群，异地多活，主机房", stacked];
        F [ label = "微服务灰度集群", stacked];
        H [ label = "微服务现网备集群，异地多活，另外一个机房", stacked];

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
        color = "orange";
        style = dashed;
        shape = line;
        }

        group slb {
        D; E;
        color = "lightgreen";
        style = dashed;
        shape = line;

        }


   }

**具体实例**

.. blockdiag::

   blockdiag double-cloud-ip {

        orientation = portrait


        A [ label = "https://www.idlepig.cn", shape = cloud, width = 220];
        B [ label = "49.4.1.2:443", shape = roundedbox];
        C [ label = "49.4.1.3:443", shape = roundedbox];
        D [ label = "10.3.1.2:8080;\n10.3.1.3:8080;\n10.3.1.4:8080;\n10.3.1.5:8080", height = 60];
        E [ label = "10.3.1.2:8080;\n10.3.1.3:8080;\n10.3.1.4:8080;\n10.3.1.5:8080", height = 60];
        G [ label = "10.6.49.9:18080,\n10.6.49.10:18080,\n10.6.49.11:18080", stacked];
        F [ label = "10.5.23.7:18080;\n10.5.23.8:18080", stacked];
        H [ label = "10.7.49.9:18080,\n10.7.49.10:18080,\n10.7.49.11:18080", stacked];

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
        color = "orange";
        style = dashed;
        shape = line;
        }

        group slb {
        D; E;
        color = "lightgreen";
        style = dashed;
        shape = line;

        }

   }

域名
    一个网站的都入口、名字。

ELB
    Elastic Load Balancer, 弹性负载均衡，让ELB后端的服务能平衡地承接用户访问的流量，主要是流量的转发。

SLB
    Software Load Balancer，软件负载均衡，使用openresty实现，openresty由nginx和lua脚本组成，主要是根据uri转发流量到不同机房、限流、灰度规则设置等等。
