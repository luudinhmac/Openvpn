# Openvpn
Mở port 
Cai dat openvpn server
Tải file trên về và cấp quyên thực thi cho nó
    chmod +x install-openvpn.sh
    ./install-openvpn.sh
    
    Chọn các tuỳ chọn, có thể để mặc định  (Phải có ip public)
    
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
    
    #chú ý: ens18 là tên card mạng(thay đổi cho phù hợp)
    - Để thêm user cetificate thì chạy file Install-openvpn.sh 
      
    # Tạo userpass cho openvpn
    useradd <username>
    passwd <username>
    # Sửa config để login bằng user/password    
    vi /etc/openvpn/server/server.conf
    thêm dòng 
    plugin /usr/lib64/openvpn/plugins/openvpn-plugin-auth-pam.so login

    Khởi động lại vpn server 
    systemctl restart openvpn-server@server
    
    Sửa file <client>.ovpn thêm vào dòng
    auth-user-pass
    
    
    ---> connect
    copy file <client>.ovpn ra máy tính client.
    sử dụng phần mềm openvpn connect import file vào để sử dụng
    
