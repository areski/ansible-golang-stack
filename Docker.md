
Deploy using Vagrant on Docker
------------------------------

$ vagrant up db --provider=docker

$ vagrant docker-logs db

$ vagrant status

missing...


Deploy using Docker Only
------------------------

1) Create a Dockerfile with your distro and SSHD.

    You can use this Dockerfile: https://github.com/areski/dockerfiles/tree/master/sshd

2) Build and run the docker container:

    docker build -t eg_sshd .
    docker run -d -P --name test_sshd eg_sshd

3) Find out on which IP / Port the container is running:

    docker port test_sshd 22

4) create file `hosts`:

    [docker1]
    127.0.0.1         ansible_ssh_port=49153     ansible_ssh_user=root

5) run the playbook:

    ansible-playbook -vvvv ansible.yml -i hosts --ask-pass

    # password by default is `screencast`

