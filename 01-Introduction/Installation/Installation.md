# Docker Installation 

A very detailed instructions to install Docker are provide in the below link

https://docs.docker.com/get-docker/

---

for Demo 
create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

```bash
sudo apt update
sudo apt install docker.io -y
```

# Start Docker and Grant Access

 Grant acess to the user they want to use to interact with docker and run docker commands.
Always ensure the docker daemon is up and running.

A easy way to verify your Docker installation is by running the below command

```bash
docker run hello-world
```
If the output says:

```bash
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

This can mean two things,

Docker deamon is not running.
Your user does not have access to run docker commands.
Start Docker daemon
use the below command to verify if the docker daemon is actually started and Active

```bash
sudo systemctl status docker
```

If you notice that the docker daemon is not running, you can start the daemon using the below command

```bash
sudo systemctl start docker
```

Grant Access to your user to run docker commands
To grant access to your user to run the docker command, you should add the user to the Docker Linux group. Docker group is create by default when docker is installed.

```bash
sudo usermod -aG docker ubuntu
```
In the above command ubuntu is the name of the user, you can change the username appropriately.

**NOTE** : Need to logout and login back for the changes to be reflected.

### Docker is Installed, up and running 

Use the same command again, to verify that docker is up and running.

```bash
docker run hello-world
```

Output should look like:

```bash
....
....
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
...
```





