```
const express = require('express');
const app = express();
const PORT = 3000;

// Simple in-memory cache object
const cache = {};

// Cache middleware
function cacheMiddleware(req, res, next) {
    const key = req.url;
    if (cache[key]) {
        console.log('Cache hit');
        res.send(cache[key]);
    } else {
        console.log('Cache miss');
        res.sendResponse = res.send;
        res.send = (body) => {
            cache[key] = body;
            res.sendResponse(body);
        };
        next();
    }
}

// Example route using the cache middleware
app.get('/data', cacheMiddleware, (req, res) => {
    // Simulate database call
    setTimeout(() => {
        res.send('Data fetched from database');
    }, 1000);
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});

```

## With Redis:

```
const redis = require('redis');
const client = redis.createClient();
const { promisify } = require('util');
const getAsync = promisify(client.get).bind(client);
const setAsync = promisify(client.set).bind(client);

// Redis cache middleware
async function redisCacheMiddleware(req, res, next) {
    const key = req.url;
    const cacheResult = await getAsync(key);
    if (cacheResult) {
        console.log('Cache hit');
        res.send(cacheResult);
    } else {
        console.log('Cache miss');
        res.sendResponse = res.send;
        res.send = async (body) => {
            await setAsync(key, body, 'EX', 10); // Expiry set to 10 seconds
            res.sendResponse(body);
        };
        next();
    }
}

// Example route with Redis caching
app.get('/data', redisCacheMiddleware, (req, res) => {
    // Simulate database call
    setTimeout(() => {
        res.send('Data fetched from database');
    }, 1000);
});

```


### Considerations for Caching

- **Cache invalidation**: Determine how and when to invalidate or update the cache, especially in dynamic applications where data changes frequently.
- **Cache granularity**: Decide the level of granularity needed for the cache. You can cache entire pages, API responses, or even smaller data units like database query results.
- **Scalability**: Ensure that your caching strategy scales with your application, especially if you expect a high load or have a distributed system.