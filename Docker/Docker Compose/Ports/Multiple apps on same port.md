When using Docker Compose, if you have multiple services that need to share the same port, Docker Compose manages the port mapping using service names and internal networking. Here's how it works:

1. **Service Naming**: Each service defined in the `docker-compose.yml` file has a unique name. Docker Compose uses these service names to create a DNS record within the Docker network.
    
2. **Internal Networking**: Docker Compose automatically creates a network for the services defined in the `docker-compose.yml` file. Services can communicate with each other using their service names as hostnames.
    
3. **Port Mapping**: When you map a port in Docker Compose, you define how ports on the host machine are mapped to ports on the containers. For example


```yaml
version: '3'
services:
  service1:
    image: my-service1-image
    ports:
      - "8080:80"
  service2:
    image: my-service2-image
    ports:
      - "8081:80"

```

In this example, `service1`'s container port 80 is mapped to the host port 8080, and `service2`'s container port 80 is mapped to the host port 8081. This way, even though both services expose the same container port (80), they are accessible via different ports on the host machine.

If multiple services need to communicate internally on the same port, they do so using their service names

```yaml
version: '3'
services:
  service1:
    image: my-service1-image
    networks:
      - my-network
  service2:
    image: my-service2-image
    networks:
      - my-network
networks:
  my-network:
    driver: bridge

```

In this case, `service1` can communicate with `service2` using the hostname `service2` and vice versa. Internally, they use the same network and can access each other on the ports exposed by their respective containers.

If you need two services to listen on the same host port, you would need to use a reverse proxy like Nginx or Traefik, which can route traffic based on the hostname or path to the appropriate service. Here’s an example using Traefik

```yaml
version: '3'
services:
  traefik:
    image: traefik:v2.0
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--entrypoints.web.address=:80"
    ports:
      - "80:80"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
  service1:
    image: my-service1-image
    labels:
      - "traefik.http.routers.service1.rule=Host(`service1.local`)"
  service2:
    image: my-service2-image
    labels:
      - "traefik.http.routers.service2.rule=Host(`service2.local`)"

```

## Using Nginx

See [[Using Nginx as Reverse Proxy with Docker Compose]]