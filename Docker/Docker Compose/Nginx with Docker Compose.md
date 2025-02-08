To add an Nginx service to your existing Docker Compose setup on a Raspberry Pi, you would generally use Nginx as a reverse proxy to manage requests to your application(s). This is particularly useful for handling static assets, SSL termination, load balancing, or simply abstracting the application layer from direct client access.

Here’s a step-by-step guide to adding an Nginx service to your Docker Compose file:

### 1. Create or Modify Your Docker Compose File

Suppose you already have a Docker Compose file for your Node.js application. You can add another service for Nginx. Here’s how your `docker-compose.yml` might look:

```javascript
version: '3.8'

services:
  app:
    build:
      context: ./some-folder/another-folder
      dockerfile: Dockerfile
    volumes:
      - ./some-folder/another-folder:/usr/src/app
      - /usr/src/app/node_modules
    networks:
      - app-network

  nginx:
    image: nginx:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/site.conf:/etc/nginx/conf.d/default.conf
      - ./some-folder/another-folder/public:/usr/share/nginx/html:ro
    depends_on:
      - app
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

```

### 2. Configure Nginx

You will need to provide Nginx configuration files. Create a folder called `nginx` in your project directory and add the following configuration files:

#### nginx.conf

This is the main Nginx configuration file. You might not need to modify the default configuration for a basic setup, but you can customize it as needed.

#### site.conf

Create a `site.conf` in the `nginx` folder to configure your server block. This file will define how Nginx handles incoming requests and proxies them to your application:

```nginx
server {
    listen 80;
    server_name your-domain.com;

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

```

This configuration does the following:

- **proxy_pass**: Routes requests to your Node.js application (listening on port 8080).
- **location /static**: Serves static files from Nginx directly, improving performance for static content.

### 3. Ensure the Nginx Image is Compatible

Make sure the Nginx image you use is compatible with the ARM architecture of your Raspberry Pi. The `nginx:latest` tag usually has ARM support, but you can explicitly use an ARM image if necessary.

### 4. Start Your Services

Run your Docker Compose to start up both the Node.js application and Nginx


```bash
docker-compose up --build

```

### 5. Accessing the Application

Now, you should be able to access your application through the Nginx reverse proxy by visiting `http://localhost` or `http://your-domain.com` if you're deploying this on a network or the internet.

### Security Considerations

If you're planning to expose your Raspberry Pi to the internet:

- Consider securing the Nginx with SSL/TLS. You can use Let's Encrypt for a free SSL certificate.
- Ensure you have proper firewall rules in place.
- Regularly update your Docker images and Raspberry Pi OS to keep your system secure.

Adding Nginx to your setup can significantly enhance your project's performance and security by managing how requests are handled and distributed.
