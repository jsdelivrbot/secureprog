
# Task 1. Tracing application ABI calls using strace #

You have several applications that do not work on Docker image. You have to create conditions (folders, files, sockets, etc) for application to run. Application considered as "running" when it outputs to stdout: "Application terminated normally".

Do the tasks under user "magistras" (on login, perform `su magistras`)

How to run:
* Install Docker
* Run:
  `docker build -t sec-pro-img https://github.com/rgrisha/secureprog.git#master:tasks/task1`
* Run Docker image:
  * `docker run --security-opt seccomp:unconfined sec-pro-img /sbin/init`
  * In another terminal issue command `docker ps` and find id of container running sec-pro-img image
* To connect to Centos Linux process, open new terminal and issue:
  * `docker exec -it <ID of container> /bin/bash`
  * Finally you are inside container that was made from image sec-pro-img for your tasks.
  * Inside container:
  * ```bash
     su magistras  
     cd ~/app[1-4]  
     ```
     And try to do the task

* Working with containers
  * To list containers:  
    ```bash
    docker ps
    ```
  * To list all containers, also dead ones (f.ex you want to reattach)
    ```bash
    docker ps -a
    ```
  * Connect to container if it was stopped previously:
    `docker start sec-pro-cont`
  * Attach container if is was killed previously:
    `docker attach sec-pro-cont`
  * Remove container and start over again (all work will be lost):
    `docker rm <Contained ID>` and run `docker run .....` from above again

## Evaluation: ##
app1 and app2 are mandatory - 8 points. App3 - +1 point, app4 - +1 point.

## Hints ##
* strace utility is most usable tool.
* nc is also usable for network for tasks that to something on network
* one of apps receives input from command line
* /etc/hosts is usable sometimes
* app3 uses gethostbyname to obtain IP address
* app4 uses realtime Mongolian Tugrik currency rate via webservice. Trying to convince Lithuanian Bank to change this rate temporarily is hard. There are more easy ways.


