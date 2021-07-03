# Redis
* Redis is an in-memory data structure store that can be used as a database, cache, or publish/subscribe client.
* In terms of WebSockets there are some ways of “sharing” the pool of open connections between many instances. One way is to use Redis’ publish/subscribe mechanism to forward emitted events between all instances of the application to make sure each open connection receives them.