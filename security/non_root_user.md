# Non-root User
A good security measure is to create a non root user in the dockerfile and at the end of it (the Dockerfile) switch to that user (USER command). This will result in that the containers commands will be run by that user. There is no way (that I know of) that you can become root again. If you extend the image in a new Dockerfile then you can switch back to root.

Why do we not want to be root? Security and permissions.

