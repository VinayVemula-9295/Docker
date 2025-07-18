# Docker Commands Cheat Sheet

### `docker images`

Lists all Docker images available locally on the host machine.

```bash
docker images
```

---

### `docker build`

Builds a Docker image from a `Dockerfile`.

```bash
docker build -t <image_name>:<tag> .
```

**Example:**

```bash
docker build -t myapp:latest .
```

---

### `docker run`

Runs a Docker container from an image.

```bash
docker run [OPTIONS] IMAGE
```

**Common options:**

* `-d` → Detached mode (run in background)
* `-p` → Port mapping (`host:container`)
* `--name` → Assign a name to the container
* `-v` → Mount volume
* `--rm` → Automatically remove container when it exits

**Example:**

```bash
docker run -d -p 8080:80 --name web nginx
```

> Use `docker run --help` to explore all available options.

---

###  `docker ps`

Lists **currently running** containers.

```bash
docker ps
```

Add `-a` to show **all** containers (running + stopped):

```bash
docker ps -a
```

---

###  `docker stop`

Stops a **running** container.

```bash
docker stop <container_id or name>
```

---

###  `docker start`

Starts a **stopped** container.

```bash
docker start <container_id or name>
```

---

###  `docker rm`

Removes a **stopped** container.

```bash
docker rm <container_id or name>
```

Use `-f` to force remove a running container:

```bash
docker rm -f <container_id>
```

---

###  `docker rmi`

Removes a Docker **image**.

```bash
docker rmi <image_id or name>
```

---

###  `docker pull`

Pulls/downloads an image from a Docker registry (like Docker Hub).

```bash
docker pull <image_name>:<tag>
```

---

###  `docker push`

Pushes an image to a Docker registry.

```bash
docker push <image_name>:<tag>
```

> Make sure you’re logged in using `docker login`.

---

###  `docker exec`

Executes a command inside a **running** container.

```bash
docker exec -it <container_name> <command>
```

**Example (open bash):**

```bash
docker exec -it mycontainer bash
```

---

### `docker network`

Manage Docker **networks**.

```bash
docker network [COMMAND]
```

**Common subcommands:**

* `ls` → List all networks
* `create` → Create a new custom network
* `rm` → Remove a network
* `inspect` → View detailed info about a network
* `connect` → Connect a container to a network
* `disconnect` → Disconnect container from a network

**Examples:**

* Create a bridge network:

```bash
docker network create my_bridge_net
```

* Run a container with a specific network:

```bash
docker run -d --name app --network my_bridge_net nginx
```

* Connect an existing container to another network:

```bash
docker network connect my_bridge_net existing_container
```

* View network details:

```bash
docker network inspect my_bridge_net
```
