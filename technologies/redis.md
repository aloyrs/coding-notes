# Redis Overview

## What is Redis?

Redis is an open-source, in-memory data structure store that serves as a highly performant and versatile solution for caching, messaging, and real-time analytics. It supports various data structures like strings, lists, sets, hashes, and more.

- Can be used as cache
- Can be used as primary database

## When to Use Redis?

Use Redis when:

- **High Performance is Crucial:** Redis excels in scenarios where fast read and write operations are essential, thanks to its in-memory storage.

- **Caching Requirements:** It's an excellent choice for caching frequently accessed data to reduce database load and improve application performance.

- **Real-time Analytics:** Redis can be used for real-time analytics and counters, such as tracking user activity or monitoring system metrics.

- **Pub/Sub Messaging:** Redis provides Pub/Sub (publish/subscribe) capabilities, making it suitable for building real-time messaging systems.

- **Session Storage:** It's often used to store session data in web applications due to its speed and simplicity.

## How to Use Redis (Example)

### Setting up a Basic Web Application with Node.js and Express

1. Install Dependencies:

   ```bash
   npm install express ioredis
   ```

2. Create Express Application (app.js):

   ```javascript
   const express = require("express");
   const Redis = require("ioredis");

   const app = express();
   const port = 3000;
   const redis = new Redis();

   app.get("/example", async (req, res) => {
     const cacheKey = "exampleData";

     // Check if data is in the Redis cache
     const cachedData = await redis.get(cacheKey);

     if (cachedData) {
       // If in cache, return cached data
       res.json({
         result: "Data from Redis Cache",
         data: JSON.parse(cachedData),
       });
     } else {
       // If not in cache, fetch data (can be from database too) and store in Redis
       const fetchData = { example: "data" };
       await redis.set(cacheKey, JSON.stringify(fetchData));
       res.json({ result: "Fresh Data from Server", data: fetchData });
     }
   });

   app.listen(port, () => {
     console.log(`Server is running on http://localhost:${port}`);
   });
   ```

3. Run the Application:

   ```bash
   node app.js
   ```

4. Test the Endpoint:

   - Open your browser and navigate to http://localhost:3000/example.

   - The example demonstrates checking for data in Redis cache. If found, it returns cached data; otherwise, it fetches fresh data (for example from database) and stores it in Redis.
