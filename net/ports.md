# Ports
You can map ports from host to container. You can also choose if it should use tcp/ip or udp (or both). You can map out a port range so you don’t have to map a lot of ports manually. The problem is that this doesn’t seem to work if you only want **udp**.

A good thing about ports is that the port on the host doesn’t  need to be the same in the container. So you can have 10 containers that have port 8080 internally but you map it out to 8080, 8081, 8082...etc. 

