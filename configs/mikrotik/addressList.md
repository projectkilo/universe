
### The following lists IPv4 addresses

/ip pool
add name=pool_management ranges=172.16.10.1-172.16.10.14
add name=pool_servers ranges=172.16.20.1-172.16.20.30
add name=pool_iot ranges=172.16.30.1-172.16.30.30
add name=pool_wifi ranges=172.16.40.1-172.16.40.254
add name=pool_office ranges=172.16.50.1-172.16.50.6
add name=pool_wireguard ranges=172.16.60.1-172.16.60.6

/ip address
add address=172.16.10.1/28 interface=vlan10 network=172.16.10.0
add address=172.16.20.1/27 interface=vlan20 network=172.16.20.0
add address=172.16.30.1/27 interface=vlan30 network=172.16.30.0
add address=172.16.40.1/24 interface=vlan40 network=172.16.40.0
add address=172.16.50.1/29 interface=ether3 network=172.16.50.0
add address=172.16.60.1/29 interface=wg1 network=172.16.60.0

/ip dhcp-server network
add address=172.16.10.0/28 gateway=172.16.10.1
add address=172.16.20.0/27 gateway=172.16.20.1
add address=172.16.30.0/27 gateway=172.16.30.1
add address=172.16.40.0/24 gateway=172.16.40.1
add address=172.16.50.0/29 gateway=172.16.50.1
add address=172.16.60.0/29 dns-none=yes gateway=172.16.60.1
