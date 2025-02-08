## Setting Up a Secure Network with Docker Compose

Follow these steps to set up a secure network using Docker Compose.

---

### 1. Create a Custom Docker Network
Docker provides built-in networking capabilities. Add a custom `bridge` network to your `docker-compose.yml`:

```yaml
networks:
  secure_network:
    driver: bridge
```

---

### 2. Use Docker Compose for Isolated Services
Example `docker-compose.yml` file with `web` and `db` services communicating over a secure network:

```yaml
version: "3.8"

services:
  web:
    image: nginx
    ports:
      - "443:443"  # Expose secure HTTPS
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro
    depends_on:
      - db
    networks:
      - secure_network

  db:
    image: postgres
    environment:
      POSTGRES_USER: secure_user
      POSTGRES_PASSWORD: secure_password
      POSTGRES_DB: secure_db
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - secure_network

volumes:
  db_data:

networks:
  secure_network:
    driver: bridge
```

This setup:
- Isolates the services in the `secure_network`.
- Exposes only the necessary `443` port to the outside world.

---

### 3. Enable HTTPS

#### 1. Create or Obtain SSL Certificates
Use [Let's Encrypt](https://letsencrypt.org/) for free SSL certificates or create self-signed certificates for testing.

#### 2. Configure NGINX for HTTPS
Create an `nginx.conf` file:

```nginx
server {
    listen 443 ssl;
    server_name yourdomain.com;

    ssl_certificate /etc/nginx/ssl/cert.pem;
    ssl_certificate_key /etc/nginx/ssl/key.pem;

    location / {
        proxy_pass http://db:5432;
    }
}
```

Place SSL certificates in `./ssl`:

```bash
mkdir ssl
mv cert.pem key.pem ./ssl
```

Update the `docker-compose.yml` file to include SSL configuration:

```yaml
volumes:
  - ./ssl:/etc/nginx/ssl:ro
```

---

### 4. Secure Database Connections

#### For Postgres:
- Use strong credentials:
  ```yaml
  environment:
    POSTGRES_USER: secure_user
    POSTGRES_PASSWORD: secure_password
  ```

- Enable SSL in `postgresql.conf`:
  ```bash
  ssl = on
  ssl_cert_file = '/path/to/server.crt'
  ssl_key_file = '/path/to/server.key'
  ```

#### For Other Databases:
- Configure them to accept only encrypted connections.

---

### 5. Restrict External Access
Use Docker Compose's `expose` directive to ensure services are only accessible within the `secure_network`:

```yaml
db:
  expose:
    - "5432"
```

---

### 6. Limit Resource Access with Docker Security Features

- Use non-root users in containers:
  ```yaml
  web:
    user: 1001:1001
  ```

- Enable read-only filesystems:
  ```yaml
  web:
    read_only: true
  ```

- Drop unnecessary Linux capabilities:
  ```yaml
  web:
    cap_drop:
      - ALL
  ```

---

### 7. Implement Network Policies (Optional)
Assign static IPs to services for more control:

```yaml
networks:
  secure_network:
    driver: bridge
    ipam:
      config:
        - subnet: "192.168.1.0/24"
```

---

### 8. Multiple Nginx Configurations for Port Mappings

To handle multiple port mappings effectively, you can organize your Nginx configurations as follows:

#### 1. Single Configuration File
Use a single configuration file for all mappings if you have a small number of services:

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://localhost:3000;
    }
}

server {
    listen 8080;
    server_name app.example.com;

    location / {
        proxy_pass http://localhost:4000;
    }
}
```

#### 2. Separate Configurations for Each Service
For scalability and maintainability, create separate configuration files:

- Create files in `/etc/nginx/sites-available/`:
  - `/etc/nginx/sites-available/service1`
  - `/etc/nginx/sites-available/service2`

- Example `service1` configuration:

```nginx
server {
    listen 80;
    server_name service1.example.com;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

- Example `service2` configuration:

```nginx
server {
    listen 8080;
    server_name service2.example.com;

    location / {
        proxy_pass http://localhost:4000;
    }
}
```

- Enable the configurations:

```bash
sudo ln -s /etc/nginx/sites-available/service1 /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/service2 /etc/nginx/sites-enabled/
```

- Reload Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

#### 3. Combining Multiple Ports in One Server Block
If services are related to the same domain, use a single server block with multiple locations:

```nginx
server {
    listen 80;
    listen 8080;
    server_name example.com;

    location /app1 {
        proxy_pass http://localhost:3000;
    }

    location /app2 {
        proxy_pass http://localhost:4000;
    }
}
```

---

### 9. Audit and Monitor Your Setup

- Use tools like `Docker Bench for Security` to audit:

  ```bash
  docker run --rm -it --net host --pid host --userns host --cap-add audit_control \
    -v /etc:/etc:ro -v /usr/bin/docker:/usr/bin/docker:ro -v /usr/lib/systemd:/usr/lib/systemd:ro \
    -v /var/lib:/var/lib:ro -v /var/run/docker.sock:/var/run/docker.sock:ro \
    docker/docker-bench-security
  ```

- Log and monitor traffic using tools like `Prometheus` and `Grafana`.

---

By implementing these practices, you create a secure and isolated network for your services using Docker Compose and configure Nginx for effective multi-port setups.
