---
title: "Configuring Docker to Use the Remote Host"
categories: ["docker", "devops"]
---


To use the remote host as your Docker host instead of your local machine, set the DOCKER_HOST environment variable to point to the remote host. This variable will instruct the Docker CLI client to connect to the remote server.

`export DOCKER_HOST=ssh://sammy@your_server_ip`
Now any Docker command you run will be run on the Droplet. For example, if you start a web server container and expose a port, it will be run on the Droplet and will be accessible through the port you exposed on the Droplet’s IP address.

To verify that you’re accessing the Droplet as the Docker host, run docker info.

`docker info`
You will see your Droplet’s hostname listed in the Name field like so:

Output
```
Name: docker-host
```
One thing to keep in mind is that when you run a docker build command, the build context (all files and folders accessible from the Dockerfile) will be sent to the host and then the build process will run. Depending on the size of the build context and the amount of files, it may take a longer time compared to building the image on a local machine. One solution would be to create a new directory dedicated to the Docker image and copy or link only the files that will be used in the image so that no unneeded files will be uploaded inadvertently.

Once you’ve set the DOCKER_HOST variable using export, its value will persist for the duration of the shell session. Should you need to use your local Docker server again, you can clear the variable using the following command:

`unset DOCKER_HOST`