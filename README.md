# devops-project

Usage:
  1. start vagrant \
    a. Run *vagrant up* for the first time, provision will be automatically run and VM is prepared, containers are started.
  2. start containers \
    Subsequent vagrant command will only bring up VM, *docker-compose -f /srv/docker-compose.yaml up -d* needs to be used to start all containers
  3. stop containers \
    docker-compose -f /srv/docker-compose.yaml down
  4. shutdown vagrant \
    *vagrant halt*
  
  *Note:* DO NOT use "vagrant destroy" after you started project work, it will delete the VM so that all data will be lost.

Vagrant:
 1. Creates vagrant box that will host jenkins, gitlab and sonarqube containers.
 2. The Vagrantfile allocates 10G memory and 4 cores of CPU to vagrant box. Note: 8G memory might work too
 3. The Vagrantfile is defined to use bridged network.
    a. During setup stage, you will be prompted to select a network to bridge: 
    
    ==> default: Available bridged network interfaces:
      1) en0: Wi-Fi (AirPort)
      2) en6: USB Ethernet(?) \
      .....
      
    b. Select the desired network using index. Desired network is usally the one that is used for Internet and DHCPed from your router.
 4. Vagrant provision will do all necessary configurations and bring up all containers
 5. Vagrant prints all IPs in the VM, which will be used to access the containers.

Docker-compose:
 Usage: 
   start: docker-compose up -d [inidividual container name]
   stop:  docker-compose down

Docker volume mapping:
  Containers are run and mounted to /srv/ inside of VM

Networking:
  Docker network is defined and used by all containers. Container name can be used as FQDN for intra-connection among containers.
  For example, inside of jenkins, you can "ssh gitlab" to access gitlab container

Ports:
  Jenkins:\
      8080:8080\
      8022:22\
  Gitlab:\
      80:80\
      443:443\
      8122:22\
  Sonarqube:\
      9000:9000
