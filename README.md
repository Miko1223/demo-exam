# demo-exam
Conf iptables
Nano /etc/iptables.sh

File:
 #!/bin/bash

export IPT="iptables"

$IPT -F
$IPT -F -t nat
$IPT -F -t mangle
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X

$IPT -P INPUT ACCEPT
$IPT -P OUTPUT ACCEPT
$IPT -P FORWARD ACCEPT

$IPT -t nat -A POSTROUTING -j MASQUERADE

/sbin/iptables-save > /etc/iptables.rules

Chmod 0740 /etc/iptables.sh

Sh /etc/iptables.sh
----------------------------------------------------------------


Включение ospf в /etc/frr/daemons (поменять 'ospf=no' на 'ocpf=yes')

Добавить в файл /etc/frr/frr.conf конфигурацию текущей сети маршрутизатора:

Log syslog informational
Router ospf
ospf router-id <ip-адрес интерфейса внутренней сети маршрутизатора или другое любое число>
network <Внутренняя сеть>/<Маска этой сети> area 0.0.0.0
network <Внешняя сеть>/<Маска этой сети> area 0.0.0.0
Перезапустить сервис frr (systemctl restart frr)

vtysh -c 'show ip ospf neighbor' – проверка
--------------------------------------------------------------
1.	Заход в конф.файл: nano /etc/default/isc.dhcp-server

File:
Inetrfacesv4=”enp0s8”

2.	Nano /etc/dhcp/dhcpd.conf
Option domain-name “hq.work”;
Option domain-name-servers 12.10.10.2,8.8.8.8

Subnet 12.10.10.0 netmask 255.255.255.192 {
Range 12.10.10.2 12.10.10.62;
Option routers 12.10.10.1;
}
Host HQ-SRV { 
Hardware ethernet MAC-ADDRESS;
Fixed-address 12.10.10.2;
}
-------------------------------------------------------------
На машине HQ-R: iperf -s
На машине ISP: iperf -c <Адрес HQ в сети HQ-ISP
-------------------------------------------------------------
7.	Настройка SSH:


2) В конфигурационном файле ( /etc/ssh/sshd_config) раскомментировать и отредактировать следующие строчки:
Port 2222
DenyUsers *@10.10.10.*

В DenyUsers знак "*" обозначает любых пользователей любого сетевого устройства данной подсети

Команда для подключения:
ssh <пользователь>@<адрес> -p <порт>
--------------------------------------------------------------------
2.	Настройка ip-forwarding
Nano /etc/sysctl.conf

File: Net.ipv4.ip_forward = 1

Sysctl – p
