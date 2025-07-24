# Docker Networking 

Docker networking allows containers to communicate with each other, the host, and external networks.   
Each container gets a virtual network interface, an IP address, and can be attached to different networks using network drivers.

Docker supports multiple types of networks. The most commonly used ones are
1) **Bridge Network**  (default for Standalone Containers)
2) **Host Network**
3) **Overlay Network**
4) **custom Network** (For Swarm Multi-host Networking)

By default, Docker provides two network drivers for you, the bridge and the overlay drivers.

## 1. Bridge Network (Default for Standalone Containers)

**What It Is**

The default network for containers on a single host.

Containers can communicate using IP addresses.

No DNS resolution by container name.

**Use Case**

Simple applications running on a single host.

When DNS-based service discovery is not needed.

**Commands**
```bash
# Run containers (attached to default bridge network)
docker run -dit --name app1 alpine
docker run -dit --name app2 alpine

# List networks
docker network ls

# Inspect the default bridge network
docker network inspect bridge

# Attempt to ping another container by name (will fail)
docker exec -it app1 ping app2

# This works( In bridge ping with IP address)
docker exec -it app1 ping <IP_ADDRESS_OF_app2>

```

#### 2. Host Network (Shares Host’s Network Stack)
**What It Is**

Container shares the host's network stack.

No NAT or IP assignment — container uses host’s IP directly.

**Use Case**

High-performance or low-latency applications (e.g., monitoring tools).

Applications requiring full network access.

**Commands**
```bash
# Run container using the host network (auto-remove container when it exits)
docker run --rm -it --network host nginx
```
**Why --rm is used**

Automatically removes the container once it stops.

Useful for temporary or debugging containers to avoid leftover stopped containers.

Keeps your environment clean without manual container cleanup.

**Limitations**  

No network isolation between host and container.

Port conflicts may occur.

### 3. Overlay Network (Multi-Host Communication)

**What It Is**  
Allows container communication across multiple Docker hosts using Docker Swarm.

Uses VXLAN tunneling.

Ideal for distributed applications.

**Use Case**  
Microservices architecture spanning multiple hosts in a Docker Swarm cluster.

**Commands**  
```bash
# Initialize Swarm mode on first node
docker swarm init

# Create overlay network
docker network create --driver overlay my_overlay

# Deploy a service to the overlay network
docker service create --name web --network my_overlay nginx
```

**Notes**  
Requires Docker Swarm mode.

Encrypted communication between hosts.

##  4. Custom Bridge Network (Improved DNS Support)
**What It Is**

Similar to the default bridge network, but with DNS-based name resolution.

Containers can communicate using container names.

**Use Case**  
Local developme
nt and multi-container applications.

Works well with Docker Compose.

**Isolation**
The Custom Bridge Network not only improves DNS-based name resolution (so containers can communicate by name) but also provides network isolation between containers that are on different custom networks.

Containers on one custom bridge network can talk to each other by name.

Containers on different custom bridge networks cannot communicate by default — this isolates traffic between groups of containers.

This isolation helps separate different projects or environments on the same Docker host.
#### commands 
```bash
# Create a custom bridge network
docker network create my_bridge_net

# Run containers on the custom network
docker run -dit --name app1 --network my_bridge_net alpine
docker run -dit --name app2 --network my_bridge_net alpine

# This ping will now work using container names
docker exec -it app1 ping app2
```
---

### Useful Commands in Networking 

### 1. **View All Networks**

```bash
docker network ls
```

---

### 2. **Inspect a Specific Network**

```bash
docker network inspect <network_name>
```

Example:

```bash
docker network inspect bridge
```

---

### 3. **Create a Custom Bridge Network**

```bash
docker network create \
  --driver bridge \
  --subnet 192.168.100.0/24 \
  custom-bridge-net
```

---

### 4. **Run a Container on a Specific Network**

```bash
docker run -dit \
  --name container1 \
  --network custom-bridge-net \
  alpine
```

---

### 5. **Connect a Running Container to Another Network**

```bash
docker network connect <network_name> <container_name>
```

Example:

```bash
docker network connect custom-bridge-net container1
```

---

### 6. **Disconnect a Container from a Network**

```bash
docker network disconnect <network_name> <container_name>
```

---

### 7. **Remove a Custom Network**

```bash
docker network rm <network_name>
```

Note: You cannot remove a network if any container is connected to it.

---

### 8. **Check Container IP Address**

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_name>
```

---

