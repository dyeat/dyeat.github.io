---
layout: post
title: "Cisco 2960X Switch 建立vlan"
date: 2019-08-08 11:30:02 +0800
categories: [others]
tags: [Cisco]
---

---

###  建立vlan 並更改名稱

※可將vlan 名稱 設定為IP位置 方便日後維護

```sh
Switch>enble
Switch#conf t
Switch(config)#vlan 10 #建立vlan 10
Switch(config-vlan)#name 192.168.10.253 #更改vlan名稱
Switch(config-vlan)#exit #退到上一層
Switch(config)#vlan 20 #建立vlan 20
Switch(config-vlan)#name  192.168.20.253 #更改vlan名稱
Switch(config-vlan)#exit #退到上一層
Switch(config)#Interface GigabitEthernet1/0/1 #設定第1 port
Switch(config-if)#switchport access vlan 10 #將第1 port轉至vlan10 區段
Switch(config-if)#exit
Switch(config)#Interface GigabitEthernet1/0/2
Switch(config-if)#switchport access vlan 10  #將第2 port轉至vlan10 區段
Switch(config-if)#exit
Switch(config)#Interface GigabitEthernet1/0/3
Switch(config-if)#switchport access vlan 20  #將第3 port轉至vlan20 區段
Switch(config-if)#exit
Switch(config)#Interface GigabitEthernet1/0/4
Switch(config-if)#switchport access vlan 20 #將第4 port轉至vlan20 區段
Switch(config-if)#exit
```

### 更改Vlan IP


#### 列出 目前vlan

```sh
Switch#show vlan
Aug  7 18:45:39.875: %SYS-5-CONFIG_I: Configured from console by consolvlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi1/0/1, Gi1/0/2, Gi1/0/3
                                                Gi1/0/4, Gi1/0/5, Gi1/0/6
                                                Gi1/0/7, Gi1/0/8, Gi1/0/9
                                                Gi1/0/10,
10   192.168.10.253                     active   Gi1/0/11, Gi1/0/12,Gi1/0/13
                                                Gi1/0/14, Gi1/0/15, Gi1/0/16
                                                Gi1/0/17, Gi1/0/18, Gi1/0/19
                                                Gi1/0/20
20   192.168.20.253                     active   Gi1/0/21, Gi1/0/22, Gi1/0/23
						 Gi1/0/24
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
```

#### 設定Vlan IP

```sh
Switch>enable
Switch#conf t
Switch(config)#conf t
Switch(config)#int vlan 1  #指定vlan1
Switch(config-if)#ip address 192.168.10.253 255.255.255.0  #設定default vlan1 IP 192.168.10.253
Switch(config-if)#exit
```

### 參考資料

[參考1](https://david50.pixnet.net/blog/post/45244986-%5B%E7%AD%86%E8%A8%98%5Dcisco%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4-vlan)
[參考2](https://admitlove2.pixnet.net/blog/post/81195293-%E8%B7%A8vlan%E5%9F%BA%E7%A4%8E%E8%A8%AD%E5%AE%9A)
[參考3](http://www.tsnien.idv.tw/Manager_WebBook/chap8/8-2%20%E5%96%AE%E4%B8%80%E4%BA%A4%E6%8F%9B%E5%99%A8%20VLAN%20%E7%B6%B2%E8%B7%AF.html)
[參考4](https://www.cyut.edu.tw/~ywfan/0909netlab/lab341.pdf)





