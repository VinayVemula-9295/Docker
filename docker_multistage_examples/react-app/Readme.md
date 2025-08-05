#### "daemon off;":
This tells Nginx to run in the foreground and not daemonize (i.e., not run as a background process).

**Why is this important?**  
By default, Nginx runs as a daemon, meaning it starts and immediately detaches from the terminal (background process).

In a Docker container, the main process must run in the foreground; otherwise, Docker thinks the process has finished and will stop the container.

Setting daemon off; keeps Nginx running as the foreground process, so the Docker container stays alive and continues serving traffic.




```bash
CMD ["nginx", "-g", "daemon off;"]
```
**means:**  
Start Nginx and keep it running in the foreground to keep the Docker container alive.

