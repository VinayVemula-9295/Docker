# Multi-Stage Builds  
### Multi-Stage Builds
A multi-stage build is a Docker technique that uses multiple FROM statements in a single Dockerfile

**When you build Docker images, you often need:**    
Build tools like npm, maven, go, gcc, etc.  
But you don't need those tools in the final production image (they bloat size & create security risks)

**Multi-stage builds let you:**  
Use one stage to compile/build the app  
Use another stage to create a clean, small image with just the final app

>Build in one stage, then  
Copy the final output to a clean, minimal image

## Comparison With vs Without Multi-Stage  
| **Build Type**      | **Image Size**  | **Contains**                      |
| ------------------- | --------------- | --------------------------------- |
| Without Multi-stage | Large (\~300MB) | Build tools, source code, and app |
| With Multi-stage    | Small (\~50MB)  | Only the final compiled app       |

### Example
```dockerfile
# Stage 1: Build stage 

FROM node:18 AS builder               # Base image with Node.js + tools (Ubuntu by default)

WORKDIR /app                         # Set working directory inside container

COPY package*.json ./ 		          # Copy only dependency files
RUN npm install      		            # Install dependencies

COPY . .              		        # Copy rest of the application code
	
# Stage 2: Production stage

FROM ubuntu:22.04                # Clean base image (no build tools), more minimal

RUN apt-get update && \
    apt-get install -y nodejs npm && \ 	  # Install only what is needed
    rm -rf /var/lib/apt/lists/* 	        #Clean up APT cache to reduce size	 

WORKDIR /app
COPY --from=builder /app .  	          # Copy built app from builder stage

EXPOSE 3000
CMD ["node", "index.js"]                  # Start app
```
**Stage 1** (builder) has all tools to install packages & build the app.

**Stage 2** only contains the final app — no npm, no cache, no build tools.

---

### Distroless Images 

Distroless images are minimal Docker images that do not contain a full Linux distribution (like Ubuntu or Alpine).  
They contain only the application and the essential runtime dependencies — nothing else.

| Feature              | Distroless Image                          |
| -------------------- | ----------------------------------------- |
|  No shell           | No `bash`, `sh`, or command line tools    |
|  No package manager | No `apt`, `yum`, `apk`                    |
|  Includes           | Just the app + required runtime libs      |
|  Smaller size       | Much smaller than base images like Ubuntu |
|  More secure        | Reduced attack surface                    |


### Why Use Distroless?
 Smaller Image Size
Less disk space, faster pulls and deployments.

Better Security
No shell or tools = fewer vulnerabilities.

Production-Only Focus
Great for final production images — not development.

### What It Does NOT Contain:
No Linux package manager like apt or apk
No shell (sh, bash)
No curl, wget, vi, nano, etc.

You cannot exec into the container and do debugging like you normally do in ubuntu or alpine images.


## Example

```dockerfile
# Stage 1: Build
FROM node:18 AS builder

WORKDIR /app
COPY . .
RUN npm install && npm run build

# Stage 2: Production using distroless
FROM gcr.io/distroless/nodejs18

WORKDIR /app
COPY --from=builder /app .

CMD ["index.js"]
```

### Explanation:
First stage (node:18) compiles and builds the app (this is your development environment).

Final image uses distroless/nodejs18 → only Node.js runtime + your app.

No shell, no npm, no bash — only your .js files and the runtime.


## Available Distroless Runtimes

From Google’s official distroless repo:
```bash
https://github.com/GoogleContainerTools/distroless
```

Common ones:

gcr.io/distroless/base

gcr.io/distroless/nodejs

gcr.io/distroless/java

gcr.io/distroless/python3

### Debugging Tip
Since there's no shell inside a distroless container, use busybox or debug versions during development, and switch to distroless for final builds.

### When to Use Distroless?
Final production deployments

Security-critical workloads

Microservices where size & security matter



