Setup docker swarm with one master and two nodes.
1.Install docker machine using below one:\
`base=https://github.com/docker/machine/releases/download/v0.16.0 && curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine && sudo mv /tmp/docker-machine /usr/local/bin/docker-machine && chmod +x /usr/local/bin/docker-machine`
  
2. `docker-machine create --driver virtualbox manager1
	docker-machine create --driver virtualbox worker1
	docker-machine create --driver virtualbox worker2`

3. `docker-machine ls`
   `docker-machine ip manager1`

4. Check whether ssh working or not.
    `docker-machine ssh manager1`
	  `docker-machine ssh worker1`
	  `docker-machine ssh worker2`
5. intialize docker swarm:

`docker swarm init --advertise-addr 192.168.99.100` (IP is the ip of master one)

6. Step 5 :  Join workers in the swarm Get command for joining as worke  In manager node run command

    `docker swarm join-token worker` This will give command to join swarm as worker.
    
7. Check whether all worker added with manager.

      `docker node ls`
    
To deploy hello world image with haproxy as LB run below commands:
1. `git clone https://github.com/Kawsar060/BS_LAB_TEST.git`
2. `cd BS_LAB_TEST/2.\ docker_swarm_haproxy_LB/`
3. `docker stack deploy -c haproxy_stack.yml haproxy`

haproxy should working as LB for hello world docker image.
