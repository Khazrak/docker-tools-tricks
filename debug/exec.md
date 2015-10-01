# exec -it bash

If you run “docker exec -it <container name or id> bash” then you will have a terminal into a container and can run commands and read files. However you might not be root (if you used Section 5 right). So for debugging purposes it might be good to wait with the non root user.

This is better then the SSH. First of all, you don’t install any unnecessary packages. Second you don’t need to map the SSH-port out and third, you take away a risk. Containers are not meant to be interactive, they should start up and then serve their service.

