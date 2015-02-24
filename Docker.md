
Deploy using Vagrant on Docker
------------------------------

$ vagrant up db --provider=docker

$ vagrant docker-logs db

$ vagrant status

missing...


Deploy using Docker Only
------------------------

1) Create a Dockerfile to run Debian 7.x with SSHD.

    docker pull tutum/debian

2) Build and run the docker container:

    docker run -d -p 2222:22 -e AUTHORIZED_KEYS="$(cat ~/.ssh/id_rsa.pub)" tutum/debian:wheezy

3) Find out on which IP / Port the container is running:

    docker ps
    docker port <docker_name> 22

4) Find the root password of the container:

    docker logs <container_id>

5) Create file `hosts`:

    [docker1]
    127.0.0.1         ansible_ssh_port=2222     ansible_ssh_user=root

6) Run the playbook:

    ansible-playbook -vvvv ansible.yml -i hosts --ask-pass
