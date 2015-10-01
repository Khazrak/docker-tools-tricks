# Dockerfile

So what differs a Dockerfile written from an experienced user from an inexperienced?
Answer: The number of Layers their Images will contain. And how do we control this?
Easy, you combine commands. So instead of running 10 RUN commands, you do 1. For it to work you need to use && between the commands. So here are two examples:

*Example 1: Bad Dockerfile*
```
FROM ubuntu:14.04
MAINTAINER Karl Andersson

ENV http_proxy="http://yourproxy.com:777"
ENV https_proxy="http://yourproxy.com:777"

    # Update Ubuntu Cache
RUN    apt-get update
    # Upgrade packages
RUN    apt-get upgrade -y
    # Install wget and unzip
RUN    apt-get install -y wget unzip
    # Download a zip file
RUN    wget http://site.com/file.zip -O /tmp/file.zip
    # Unzip zip file
RUN    unzip /tmp/file.zip
    # Remove zip
RUN    /tmp/file.zip
    # Move file
RUN    mv /tmp/file/file.txt /opt/file.txt

CMD    less /opt/file.txt

```

*Example 2: Better Dockerfile*
```
FROM ubuntu:14.04
MAINTAINER Karl Andersson

ENV http_proxy="http://yourproxy.com:777" \
https_proxy="http://yourproxy.com:777"

    # Update Ubuntu Cache
RUN    apt-get update && \
    # Upgrade packages
    apt-get upgrade -y && \
    # Install wget and unzip
    apt-get install -y wget unzip && \
    # Download a zip file
    wget http://site.com/file.zip -O /tmp/file.zip && \
    # Unzip zip file
    unzip /tmp/file.zip && \
    # Remove zip
    /tmp/file.zip && \
    # Move file
    mv /tmp/file/file.txt /opt/file.txt

CMD    less /opt/file.txt
```

*Layers:*
The Bad Dockerfile creates at least 10 layers when it builds the Image. Every ENV and RUN command becomes a separate layer. 
*Virtual Size:*
Another bad thing about the Bad Dockerfile is that if the download of a file is in one layer and the unzip and remove is in another the size will not go down even if we remove the zip.
If you do the download, unzip and remove of zip file in one command, then only the size of the unzipped file will be left.
*Explanation:*
&& in linux runs another command after the first has finished, if you only use one & then the commands are run at parallel. The \ is so we don’t have to write the command on one line (like a newline character).

