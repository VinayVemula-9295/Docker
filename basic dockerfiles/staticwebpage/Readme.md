### What is NGINX?
NGINX is a powerful, fast web server that can:

* Serve static websites (HTML, CSS, JS files)

* Reverse proxy APIs or apps

* Load balance traffic

In this case, you’ll use it to serve a static website.

## NGINX Docker Image Structure
When you pull nginx or nginx:alpine, it has:

**Internal directory structure:**
| Path                             | Purpose                                      |
| -------------------------------- | -------------------------------------------- |
| `/usr/share/nginx/html`          | Default root directory for web files         |
| `/etc/nginx/nginx.conf`          | Main config file                             |
| `/etc/nginx/conf.d/default.conf` | Default site config (included in nginx.conf) |
| Port `80`                        | Default HTTP port NGINX listens to           |


Build and Run the Docker Image

```bash
docker build -t my-static-website .
```
```bash
docker run -d -p 8080:80 my-static-website
```

Then open your browser and go to:

```arduino
http://localhost:8080
```

