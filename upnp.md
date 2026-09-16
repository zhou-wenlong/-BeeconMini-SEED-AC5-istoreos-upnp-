```
由于之前绑定到默认br-lan 路由器默认VLAN(192.168.88.1)
uci set upnpd.config.listening_ip='br-lan'
uci set upnpd.config.internal_iface='lan'

之前的配置
root@BMoS3:/var/etc# cat miniupnpd.conf.bak
ext_ifname=pppoe-wan
ext_ifname6=pppoe-wan
listening_ip=br-lan
enable_natpmp=yes
enable_upnp=yes
secure_mode=yes
system_uptime=yes
force_igd_desc_v1=yes
ext_perform_stun=no
ipv6_disable=no
force_forwarding=yes
bitrate_down=737280000
bitrate_up=245760000
lease_file=/var/run/miniupnpd.leases
notify_interval=300
port=5000
uuid=c43b7b65-cae6-4261-aec3-c0113c676cde
allow 0-65535 192.168.8.20/32 0-65535 #PCDN192.168.8.20
allow 0-65535 192.168.8.40/32 0-65535 #PCDN192.168.8.40
allow 0-65535 192.168.8.30/32 0-65535 #PCDN192.168.8.30
allow 0-65535 192.168.8.50/32 0-65535 #PCDN192.168.8.50
deny 1024-65535 0.0.0.0/0 1024-65535 #Allow high ports
deny 0-65535 0.0.0.0/0 0-65535 #Default deny
upnp_table_name=fw4
upnp_nat_table_name=fw4
upnp_forward_chain=upnp_forward
upnp_nat_chain=upnp_prerouting
upnp_nat_postrouting_chain=upnp_postrouting

更改为自建vlan8(192.168.8.1)
#命令行执行
uci set upnpd.config.listening_ip='br-lan8'
uci set upnpd.config.internal_iface='lan2'
uci commit upnpd
/etc/init.d/miniupnpd restart
/etc/init.d/miniupnpd status

root@BMoS3:/var/etc# cat /var/etc/miniupnpd.conf
ext_ifname=pppoe-wan
ext_ifname6=pppoe-wan
listening_ip=br-lan8
enable_natpmp=yes
enable_upnp=yes
secure_mode=yes
system_uptime=yes
force_igd_desc_v1=yes
ext_perform_stun=no
ipv6_disable=no
force_forwarding=yes
bitrate_down=737280000
bitrate_up=245760000
lease_file=/var/run/miniupnpd.leases
notify_interval=300
port=5000
uuid=c43b7b65-cae6-4261-aec3-c0113c676cde
allow 0-65535 192.168.8.20/32 0-65535 #PCDN192.168.8.20
allow 0-65535 192.168.8.40/32 0-65535 #PCDN192.168.8.40
allow 0-65535 192.168.8.30/32 0-65535 #PCDN192.168.8.30
allow 0-65535 192.168.8.50/32 0-65535 #PCDN192.168.8.50
deny 1024-65535 0.0.0.0/0 1024-65535 #Allow high ports
deny 0-65535 0.0.0.0/0 0-65535 #Default deny
upnp_table_name=fw4
upnp_nat_table_name=fw4
upnp_forward_chain=upnp_forward
upnp_nat_chain=upnp_prerouting
upnp_nat_postrouting_chain=upnp_postrouting

head -50 /var/run/miniupnpd.leases
```
<img width="580" height="589" alt="image" src="https://github.com/user-attachments/assets/683fc824-7f7f-49c5-8539-867ed3690c5a" />
