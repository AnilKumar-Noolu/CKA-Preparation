## Record Types
1. A Record: This record is mainly used for mapping IPv4 ip addresses to hostnames.
2. AAAA Record: This record is mainly used for mapping IPv6 ip addresses to hostnames.
3. CNAME: This record is used for mapping one domain name to another domain name.

### commands
1. nslookup: This command is used to query a hostname from a web server.
   Ex: nslookup www.google.com
2. dig: This command returns more details in similar form.
3. curl: This command is used transfer data to or from a server.

## Docker Networking
There are mainly 3 types of Networking available in Docker.
1. None Network
2. Host Network: This network listens on some particular port.
3. Bridge Network: In this type of Network, an internal private Network is created, which the DockerHosts and containers attach to. The Network has an address 172.17.0.0 by default and each device connecting to this Network gets their own private Network address on thsi network.

 ## Pod Networking
 - CRI defines responsibilities of Container Runtime(CR).
 - CR must create Network Namespace.
 - Conatiner Network Interface(CNI) is configured on kubelet.service ( u can check that by ps -aux | grep kubelet)
 - CNI are configured at /opt/cni/bin
 - To find CNI plugin configured to use on this cluster, check at /etc/cni/net.d

## IP Address Management
CNI responsibilities includes:
1. Must support arguments ADD/DEL/CHECK
2. Must support parameters like container id, network namespace..
3. Must support IP Address assignement to Pods.
