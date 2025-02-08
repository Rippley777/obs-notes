
To configure Nginx to proxy requests to different backend services running on various ports, you will need to set up multiple server blocks or location blocks within a single server block in your Nginx configuration file. Each block will direct traffic to a specific port based on either the requested URL or the server name. Below, I'll show you how to configure Nginx using location blocks within a single server block to proxy to different ports.

### Scenario Setup

Imagine you have two applications running in your Docker environment:

- **App1**: Running on port 8081
- **App2**: Running on port 8082

You want Nginx to route traffic to these applications based on the URL path: `http://your-domain.com/app1` for App1 and `http://your-domain.com/app2` for App2.

### Step 1: Create an Nginx Configuration File

Create a new Nginx configuration file or edit an existing one. If you're setting this up in a Docker environment, you might place this file in a directory that will be mounted to your Nginx container.

### Step 2: Configure Location Blocks

Here’s how you can edit your Nginx configuration to proxy requests to different ports based on the requested URL path:

```yaml
server {
    listen 80;
    server_name your-domain.com;

    location /app1 {
        proxy_pass http://localhost:8081;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /app2 {
        proxy_pass http://localhost:8082;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```

### Explanation of the Configuration

- **`proxy_pass`**: Directs requests to the specified URL. Note that `localhost` refers to services running on the same network as Nginx, usually within the same Docker network setup.
- **`proxy_http_version`**: Ensures HTTP/1.1 is used for the proxy.
- **Headers**:
    - `Upgrade` and `Connection` are used primarily for WebSocket support.
    - `Host` and other `X-` headers ensure that the request is forwarded correctly and that the original request information is preserved.

### Step 3: Run or Reload Nginx

- If you’re editing this file directly within a running Nginx container, you can reload Nginx to apply the changes:

```bash
nginx -s reload

```

- If you’re setting this up in Docker Compose, make sure to rebuild your Nginx container if necessary and restart it to load the new configuration.

### Accessing the Services

With this configuration, visiting `http://your-domain.com/app1` in a browser would direct the request to the service running on port 8081, and visiting `http://your-domain.com/app2` would direct the request to the service running on port 8082.

This setup is particularly useful in a microservices architecture or in a development environment where multiple services are running on different ports, and you need a single entry point to access them.



To add another port to your Nginx configuration, you typically define another `server` block that listens on the new port and configures it according to your needs. This setup allows Nginx to handle requests on multiple ports, each possibly serving different content or applications.

### Scenario Setup

Assuming you want to add a new port, say `8088`, to serve a different application or different content, here’s how you can modify your Nginx configuration:

### Step 1: Modify Your Existing Nginx Configuration

You will add another `server` block in the same configuration file that listens on the new port. Here is an example based on your current setup

```nginx
server {
    listen 80;
    server_name 99.97.209.132;

    location / {
        proxy_pass http://app:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    location /static {
        alias /usr/share/nginx/html;
        expires 30d;
    }
}

server {
    listen 8088;
    server_name 99.97.209.132;

    location / {
        proxy_pass http://app:8081;  // Assuming you have another app running on this port
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    location /static {
        alias /usr/share/nginx/html;
        expires 30d;
    }
}

```

### Explanation of the New Configuration

- The new `server` block is almost identical to the original, but it listens on port `8088` and proxies to a potentially different application (`http://app:8081`).
- Adjust the `proxy_pass` to match the internal network name and port of the application you wish to serve on this new port.
- You can also change or adjust the static content handling under the `location /static` if necessary.

### Step 2: Apply the Configuration Changes

Once you've added the new `server` block:

- **Reload Nginx** to apply the changes without restarting the service:

```bash
nginx -s reload

```

- This command tells Nginx to re-read its configuration files and apply the new settings without dropping existing connections.

### Step 3: Test the Configuration

- Ensure that there are no syntax errors in your configuration file

```bash
nginx -t

```

- If the test is successful, it will say something like `syntax is okay` and `test is successful`.
- Access your applications by visiting `http://99.97.209.132` for the app on port `80` and `http://99.97.209.132:8088` for the app served on port `8088`.

### Final Notes

This setup allows Nginx to listen on multiple ports, each configured to serve potentially different applications. It’s a flexible way to handle multiple services on a single server and is commonly used in environments where different services need to be isolated or differentiated by port.
