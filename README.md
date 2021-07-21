# Openvpn
Cai dat openvpn server


    ./install-openvpn.sh
    
    Chọn các tuỳ chọn, có thể để mặc định
    
    
    - Routing để lớp mạng vpn có thể liên lạc được với LAN bên trong
    yum upgrade -y
    yum install iptables-services -y
    systemctl mask firewalld
    systemctl enable iptables
    systemctl stop firewalld
    systemctl start iptables
    iptables --flush
    iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o ens18 -j MASQUERADE
    iptables-save > /etc/sysconfig/iptables
    systemctl restart network.service 
    
    - Để thêm user cetificate thì chạy file Install-openvpn.sh 
    
    
    ### Sửa config để login bằng user/password
    vi /etc/openvpn/server/server.conf
    thêm dòng 
    plugin /usr/lib64/openvpn/plugins/openvpn-plugin-auth-pam.so login

    Khởi động lại vpn server 
    systemctl restart openvpn-server@server
    
    Sửa file client thêm vào
    auth-user-pass
    
    
    ---> login
    
