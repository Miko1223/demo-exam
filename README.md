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
