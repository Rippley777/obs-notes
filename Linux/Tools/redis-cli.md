command-line utility used to interact with the Redis server is **`redis-cli`**.

### Common uses of `redis-cli`:

- **Connecting to a Redis server:**


- `redis-cli SET key value redis-cli GET key redis-cli KEYS *`
    

### Additional tools:

- **`redis-benchmark`**: For testing Redis performance.
- **`redis-check-aof` and `redis-check-rdb`**: For troubleshooting and verifying the integrity of Redis persistence files.




`INFO <category>`

Examples of categories:

- `server`: General information about the Redis server (e.g., version, OS).
- `clients`: Details about connected clients.
- `memory`: Memory usage statistics.
- `persistence`: Persistence-related info (e.g., RDB and AOF status).
- `stats`: General statistics (e.g., commands processed, key hits/misses).
- `replication`: Replication-related details.
- `cpu`: CPU usage stats.
- `keyspace`: Keyspace statistics.

# Server
redis_version:6.2.6
redis_git_sha1:00000000
redis_git_dirty:0
os:Linux 5.4.0-42-generic x86_64
...

# Clients
connected_clients:10
client_longest_output_list:0
client_biggest_input_buf:0
...

# Memory
used_memory:857600
used_memory_human:837.50K
...
