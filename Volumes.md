
# Docker Volumes and Bind Mounts

## Problem Statement
It is a very common requirement to persist the data in a Docker container beyond the lifetime of the container. However, the file system
of a Docker container is deleted/removed when the container dies. 

Docker containers are ephemeral by nature — when a container stops or is removed, any data stored inside it is lost. This presents a challenge when:

* You want to persist application data (e.g., databases, logs).
* You want to share data between containers.
* You want the container to survive restarts without losing data.

##  Docker’s Solution to Data Persistence

Docker provides **two primary mechanisms** to persist and manage data:

1. **Volumes** (Recommended for most use cases)
2. **Bind Mounts** (For development or advanced scenarios)

---

## Docker Volumes
A Docker-managed storage area on the host system. You can use it to persist container data independent of the container lifecycle.

Volumes are directories managed by Docker and stored in a part of the host filesystem (`/var/lib/docker/volumes/` on Linux by default). Volumes are:

* Created and managed via Docker CLI/API.
* Persisted even if the container is deleted.
* Isolated from the host OS file structure.
* Easier to back up, restore, and migrate.

###  Creating a Volume

```bash
docker volume create mydata
```

###  Using a Volume in a Container

```bash
docker run -it -v mydata:/app/data ubuntu /bin/bash
```

Inside the container, any data written to `/app/data` will be stored in the `mydata` volume.

###  Inspecting Volumes

```bash
docker volume inspect mydata
```
This command gives you detailed JSON output about a specific Docker volume, such as where it's stored, how it's used, and driver details.

###  Removing a Volume

```bash
docker volume rm mydata
```

> Note: You cannot remove a volume if it is currently in use by a container.

---

##  Bind Mounts (Host Directory Mounts)
A direct mapping between a specific path on your host and a path in the container. 
**or**
Bind mounts allow you to mount a specific path from the host machine into the container. This is useful when you need real-time access to files on your host system (e.g., during local development).

### Example

```bash
docker run -it -v /home/user/logs:/var/log/app ubuntu /bin/bash
```

This command mounts `/home/user/logs` on the host to `/var/log/app` in the container.

---

## Volumes vs Bind Mounts

| Feature            | Volumes                             | Bind Mounts                     |
| ------------------ | ----------------------------------- | ------------------------------- |
| Managed by Docker  |  Yes                                |  No                             |
| Path Location      | Docker-managed                      | User-specified on host          |
| Ease of Backup     | Easy                                |  Manual                         |
| Security Isolation | Better                              |  Direct access to host          |
| Portability        |  High                               | Low                             |
| Typical Use Cases  | Production, databases, cloud setups | Local dev, testing shared files |

---

##  Best Practices

* Use **volumes** for production workloads or when portability and data lifecycle control matter.
* Use **bind mounts** for quick iterations in local development environments.
* Prefer `--mount` over `-v` for more clarity in production-grade scripts:

```bash
docker run --mount type=volume,source=mydata,target=/data ubuntu
```


