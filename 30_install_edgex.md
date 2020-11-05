[To README](README.md)

# 3. How to install EdgeX with a virtual device service

All the tools to run EdgeX services is ready. A EdgeX stack consists of many docker containers but users don't need to launch one by one since the EdgeX team offers Docker-compose files per each release iteration. 

<br/>

## 3.1 Launch EdgeX core services

The compose files can be found from a repository - [edgexfoundry/developer-scripts](https://github.com/edgexfoundry/developer-scripts). In this chapter, the Geneva version will be used as it is the latest stable version. To launch containers:
```sh
$ cd ~

# Let's store all repositories in a directory to organize the home directory.
$ mkdir repo
$ cd repo

# Clone the developer-scripts repository
$ git clone https://github.com/edgexfoundry/developer-scripts
$ cd developer-scripts/releases/geneva/compose-files
$ ls
README.md
docker-compose-geneva-redis-no-secty-arm64.yml
docker-compose-geneva-redis-no-secty.yml
docker-compose-geneva-redis-arm64.yml
docker-compose-geneva-redis.yml
docker-compose-geneva-mongo-no-secty-arm64.yml
docker-compose-geneva-mongo-no-secty.yml
docker-compose-geneva-mongo-arm64.yml
docker-compose-geneva-mongo.yml
docker-compose-geneva-ui-arm64.yml
docker-compose-geneva-ui.yml
docker-compose-portainer.yml

# There are several compose files but don't need to use everything to launch for our purpose. First of all, ARM64 version should be used for RPI. Redis is the choice of DB because of license matter. Security is out of scope in this tutorial. Running this commands takes some time depends on the network.
$ docker-compose -f docker-compose-geneva-redis-no-secty-arm64.yml up -d
...
Creating edgex-redis       ... done
Creating edgex-core-consul ... done
Creating edgex-support-scheduler     ... done
Creating edgex-support-notifications ... done
Creating edgex-core-metadata         ... done
Creating edgex-core-command                   ... done
Creating edgex-core-data             ... done
Creating edgex-app-service-configurable-rules ... done
Creating edgex-device-virtual                 ... done
Creating edgex-sys-mgmt-agent                 ... done
Creating edgex-device-rest                    ... done
Creating edgex-kuiper                         ... done

# Once launching is done, let's check what are up and running. Some columns are removed.
$ docker ps | less -ESX
IMAGE                                                      STATUS       
emqx/kuiper:0.4.2-alpine                                   Up 11 seconds
edgexfoundry/docker-sys-mgmt-agent-go-arm64:1.2.1          Up 15 seconds
edgexfoundry/docker-device-rest-go-arm64:1.1.1             Up 14 seconds
edgexfoundry/docker-device-virtual-go-arm64:1.2.2          Up 15 seconds
edgexfoundry/docker-app-service-configurable-arm64:1.2.0   Up 14 seconds
edgexfoundry/docker-core-command-go-arm64:1.2.1            Up 18 seconds
edgexfoundry/docker-core-data-go-arm64:1.2.1               Up 19 seconds
edgexfoundry/docker-core-metadata-go-arm64:1.2.1           Up 21 seconds
edgexfoundry/docker-support-scheduler-go-arm64:1.2.1       Up 23 seconds
edgexfoundry/docker-support-notifications-go-arm64:1.2.1   Up 22 seconds
arm64v8/redis:5.0.8-alpine                                 Up 26 seconds
edgexfoundry/docker-edgex-consul-arm64:1.2.0               Up 26 seconds
portainer/portainer
```

<br/>

The names of the launched services might be familiar if we think about the diagram:

![EdgeX Architecture Diagram (Jun/12 2020)](./assets/EdgeX-Arch-Jun12-20.png.jpg)

There are the core services in the middle. Devices services will talk to the hardwares. Supporting services will inject business rules and run actions scheduled. Application services will interact with frontend and/or external cloud services. All the well considered services are just launched with one line!

<br/>

## 3.2 Test EdgeX services with Curl 

Although the services are launched well, it is worth to test the servcies before writing any custom service.

Curl is a command line tool of *nix systems to transfer data to a given URL and the basic tool to ping EdgeX services:
```
$ curl http://localhost:48080/api/v1/ping
pong

$ curl http://localhost:48081/api/v1/ping
pong

$ curl http://localhost:48082/api/v1/ping 
pong
```

Also docker-compose can be used to monitor logs:
```sh
$ docker-compose -f docker-compose-geneva-redis-no-secty-arm64.yml logs -f {data|command|metadata}
```

Lastly, the local web service "portainer" can be launched to monitor EdgeX services but it is not a command line tool so that let's use a web browser from the host machine. Before launch it, we need to edit a line in the compose file:
```sh
# Open and edit the "docker-compose-portainer.yml" 
# and update a line under the ports section from -"127.0.0.1:9000:9000" to - "9000:9000"
$ vi docker-compose-portainer.yml

# Then launch it with this command
$ docker-compose -f docker-compose-portainer.yml up -d
```

Now we can access the portainer web service with RPI's address and port number 9000 in the host's browser. For the first time access, we need to set a new password. With the Portainer UI, we can monitor the log and interact with each service. 

![Portainer](./assets/portainer.png)

<br/>

EdgeX stack is up and running so that we can start making our own custom device and app services. 

<br/>

---

Next: [How to develop custom device and app services](40_custom_services.md)