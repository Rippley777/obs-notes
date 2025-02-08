Using Nginx as a reverse proxy to route traffic to different services based on hostname or path is a common approach. Here’s how you can set this up using Docker Compose:

1. **Create a `docker-compose.yml` file** with your services and Nginx


```yaml
version: '3.8'
services:
  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - service1
      - service2

  service1:
    image: my-service1-image
    container_name: service1

  service2:
    image: my-service2-image
    container_name: service2

networks:
  default:
    external:
      name: my-network

```

**Create an `nginx.conf` file** to configure Nginx as a reverse proxy. This file should be in the same directory as your `docker-compose.yml` file:


```nginx
http {
    upstream service1 {
        server service1:80;
    }

    upstream service2 {
        server service2:80;
    }

    server {
        listen 80;

        server_name service1.local;
        location / {
            proxy_pass http://service1;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

    server {
        listen 80;

        server_name service2.local;
        location / {
            proxy_pass http://service2;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}

```

**Update your hosts file** to resolve the custom hostnames (`service1.local` and `service2.local`) to your local machine. On most systems, this can be done by editing the `/etc/hosts` file (or `C:\Windows\System32\drivers\etc\hosts` on Windows) and adding the following lines:

```lua
127.0.0.1 service1.local
127.0.0.1 service2.local

```



```bash
docker-compose up -d

```

With this setup:

- Nginx listens on port 80 on the host machine.
- Requests to `http://service1.local` are routed to `service1`.
- Requests to `http://service2.local` are routed to `service2`.

### Testing the Setup

To test the setup, you can open your browser and navigate to `http://service1.local` and `http://service2.local`. Each should direct you to the respective service.

### Additional Configuration

- **Environment-specific configuration**: You might want to handle different environments (development, staging, production) by having separate Nginx configurations or using environment variables.
- **SSL/TLS**: For a production setup, you should configure SSL/TLS. You can use Let's Encrypt with a tool like `certbot` to automate SSL certificate generation and renewal.
- **Load Balancing**: If you have multiple instances of the same service, you can add more servers to the upstream block, and Nginx will load balance requests between them.

Here’s an example of load balancing within the `nginx.conf`

```nginx
upstream service1 {
    server service1:80;
    server service1-2:80;
}

upstream service2 {
    server service2:80;
    server service2-2:80;
}

```

Ensure that the additional service instances are defined in your `docker-compose.yml`

```yaml
  service1-2:
    image: my-service1-image
    container_name: service1-2

  service2-2:
    image: my-service2-image
    container_name: service2-2

```

This configuration balances the load between `service1` and `service1-2` as well as `service2` and `service2-2`.
