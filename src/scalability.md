# Scalability

*Infinite lines stretch, Whispers grow into a roar— Silence holds the weight.*

## Scalable Architecture

**Horizontal**: adding more machines to handle the load (like buildings)
**Vertical**: adding more power to those machines

### Components of a scalable system
1. Load balancers
2. Cache process
3. Queuing of requests

## Questions

*Explain how you would distribute load and ensure high availability.*
1. Have load balancing infrastructure in place that distribute requests to different servers. (geographical/edge stuff with NextJS)
2. Have a backup system, redundancy

*Describe the use of caching to reduce database load.*
1. Instead of querying for the same data multiple times, you can query it once and store it in a cache (browser cache, react-query). Some systems have things in place to do this automagically (Nextjs and Vercel ISR)