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


## Now the sample or fist docker File which is in the Example folder 


### Clone this repository and move to example folder

```bash
git clone https://github.com/VinayVemula-9295/Docker.git
```

then 

```bash
cd Docker/example/first-docker-file
```

### Login to Docker

```bash
docker login -u vinay9295
```

Then enter your password when prompted.

After a successful login, you’ll see:

```bash
Login Succeeded
```

### Build your first Docker Image

```bash
docker build -t vinay9295/my-first-docker-image:latest .
```

Here **vinay9295** is the dockerhub-username

Output of the above command
```bash
    Sending build context to Docker daemon  992.8kB
    Step 1/6 : FROM ubuntu:latest
    latest: Pulling from library/ubuntu
    677076032cca: Pull complete
    Digest: sha256:9a0bdde4188b896a372804be2384015e90e3f84906b750c1a53539b585fbbe7f
    Status: Downloaded newer image for ubuntu:latest
     ---> 58db3edaf2be
    Step 2/6 : WORKDIR /app
     ---> Running in 630f5e4db7d3
    Removing intermediate container 630f5e4db7d3
     ---> 6b1d9f654263
    Step 3/6 : COPY . /app
     ---> 984edffabc23
    Step 4/6 : RUN apt-get update && apt-get install -y python3 python3-pip
     ---> Running in a558acdc9b03
    Step 5/6 : ENV NAME World
     ---> Running in 733207001f2e
    Removing intermediate container 733207001f2e
     ---> 94128cf6be21
    Step 6/6 : CMD ["python3", "app.py"]
     ---> Running in 5d60ad3a59ff
    Removing intermediate container 5d60ad3a59ff
     ---> 960d37536dcd
    Successfully built 960d37536dcd
    Successfully tagged abhishekf5/my-first-docker-image:latest
```

### Verify Docker Image is created

```bash
docker images
```
Output

```bash
REPOSITORY                         TAG       IMAGE ID       CREATED          SIZE
vinay9295/my-first-docker-image   latest    960d37536dcd   26 seconds ago   467MB
ubuntu                             latest    58db3edaf2be   13 days ago      77.8MB
hello-world                        latest    feb5d9fea6a5   16 months ago    13.3kB
```

#### Run your First Docker Container

```bash
docker run -it vinay9295/my-first-docker-image
```

Output

Hello World

---
### Push the Image to DockerHub and share it with the world

```bash
docker push vinay9295/my-first-docker-image
```

Output
```bash

Using default tag: latest
The push refers to repository [docker.io/vinay9295/my-first-docker-image]
35f7f16e667c: Pushed
62f1c4990a09: Pushed
d908a1cfe9b6: Pushed
107cbdaeec04: Mounted from library/ubuntu
latest: digest: sha256:20f4fa6060aeb0e873c82f4dbf45962c893042f7412c9b4e0797a41a46a88f52 size: 1155

```












