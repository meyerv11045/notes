### Microservice Architectual Style:

- Developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanics, often an HTTP resource API
- Encourages modularity and seperation of concerns
- ability to horizontally scale and partition the workload
- Microservices contain many aspects in reality:
  - Clients, Caches, and Databases are all included in a microservice in conjuction with the service itself

### Stateless Service:

- Not a cache or database
- Frequently accessed metadata
- no instance affinity
- Losing a node is not a big deal and can be easily fixed

### Stateful Service:

- Databases & caches
- Custom apps which holds lots of data
- Losing a node is a notable event and it might take hours to get it fixed