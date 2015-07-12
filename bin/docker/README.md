# Docker Container Utility Scripts

All scripts provided in the above bin directory provide a dynamic way of using consul as a DNS with applications inside of the docker container.
This scripts were exclusively targeted toward OSX but can be adjusted for linux.

```
boot2docker init
boot2docker up
docker-consul
docker-configure-dns
```

Now, there should be an instance of consul running in the docker container.
You should be able to access conul in the browser through http://consul:8500/ui.

To add a new application to consul, swap your typical `docker run` command with `docker-run`.
This is a simple wrapper around the basic `docker run` command but adds the consul instance as a dns entry.

```
docker-destroy ${container_name}
docker-run \
    --name="${container_name}" \
    --hostname="${container_name}" \
    -v ${PROJECT_DIR}/static:/usr/local/apache2/htdocs/ \
    httpd:2.4
docker-consul-register ${container_name}
```

Once a container has been built, run, and registered, you should be able to navigate to the container in a browser using the container name.
It should be noted that when you access applications in the browser, you will still need to add the port to the end of the container name.
