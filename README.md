Block incoming Ping

iptables -A INPUT -p icmp --icmp-type echo-request -j REJECT

Allow updates [HTTP/HTTPS] / Apache 

iptables -A OUTPUT -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --sport 80 -m state --state ESTABLISHED -j ACCEPT
iptables -A INPUT -m state --state NEW -p tcp --dport 443 -j ACCEPT

Block outgoing connections 

iptables -A OUTPUT -o eth1 -j DROP

Bind9

iptables -A OUTPUT -d DNSServer -p udp -dport 53 -j ACCEPT
iptables -A INPUT -s DNSServer -p udp -sport 53 -j ACCEPT

ProFTPd

iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -I INPUT 2 -p tcp --match multiport --dports 49152:65535 -j ACCEPT

