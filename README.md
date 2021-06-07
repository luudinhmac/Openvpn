# Openvpn
Cai dat openvpn server

 yum upgrade -y
    yum install iptables-services -y
    
    systemctl mask firewalld
    
    systemctl enable iptables
   
    systemctl stop firewalld
    systemctl start iptables
    iptables --flush
