# net=host

net=host is a run command flag that configures the container to use the hosts existing network stack instead of creating a new. Now this can solve some problems:
* Multicast support
* Talking to non dockerized apps
But it also comes with a lot of problems:
* You can’t link that container to another container
* Containers that want to talk to that container also has to have net=host
Port mapping (eg. 8090:8080) doesn’t work (since it’s a network thing)
I would only use net=host if you have a problem with authentication (eg. LDAP) or Multicast problem (this you can solve with Weave or similar)
