# Lesson 12: Applications (CDNs and Overlay Networks)
- What is the drawback to using the traditional approach of having a single, publicly accessible web server?
    - Long geographic distance causing performance issues
    - Wastful repetition of sending the same viral content increases bandwitdth costs
    - The system being a single point of failure

- What is a CDN?
    - Content Distribution Networks are networks of multiple, geographically distributed severs and/or data centers that stores copies of content and directs users to the server that can best fulfill their requests.

- What are the six major challenges that Internet applications face?
    - Peering point congestion
    - Inefficient routing protocols
    - Unreliable networks
    - Inefficient communication protocols
    - Scalability
    - Application limitations and slow rate of change adoption

- What are the major shifts that have impacted the evolution of the Internet ecosystem?
    - Increased demand for online content
    - The topological flattening of the network from a hierarchical structure to a flatter one with more IXPs

- Compare the “enter deep” and “bring home” approach to CDN server placement.
    - The "enter deep" approach uses many smaller sever clusters placed deep in the access networks to reduce user delay and increase throughput, but it's harder to manage
    - The "bring home" approach uses fewer, larger clusters at key points (IXPs), which is easier to manage but results in higher delay and lower throughput for users.

- What is the role of DNS in the way CDN operates?
    - To intercept the user's request for content by redirecting the hostname asscoiated with the content provider to a hostname in the CDN domain. This allows the CDN's name server system to ultimately return the IP address of the most appropriate CND content server to the user.

- What are the two main steps in CDN server selection?
    - Intercepting the user's request using DNS rediction to CDN's name server
    - Deciding the IP address of the content server to return to the user

- What is the simplest approach to selecting a cluster? What are the limitations of this approach?
    - Use geolocation-based mapping, which directs the user to the cluster geographically closet to them.

- What metrics could be considered when using measurements to select a cluster?
    - Network-layer metrics, such as delay and available bandwidth
    - Application-layer metrics, such as rebuffering ratio, average bitrate, or page load time

- How are the metrics for cluster selection obtained?
    - Active measurements: Local DNS Server (LDNS) probing multiple clusters
    - Passive measurements: the CDN's name server system tracking performance metrics based on existing session traffic

- Explain the distributed system that uses a 2-layered system. What are the challenges of this system?
    - The distributed 2-layered system has a slow, big picture layer that makes a general quality prediction model, and a fast, per-user layer that makes the actual server choice based on that model and the client's live status
    - The challeges are:
        - It's difficult to manage a single central control point that knows all network conditions in real time
        - They must intentially send some users to bad clusters just to collect the necessary data to build the models

- What are the strategies for server selection? What are the limitations of these strategies?
    - Random assignment: not optimal because it might select a highly loaded server
    - Load balancing: not optimal because a less-loaded sever might not have the requested content cached, so the client will see a higher delay and there will be unnecessary requests to the origin server
    - Content-based hashing: the cluster is dynamic. If a machine fails, the hash table needs to be recomputed

- What is consistent hashing? How does it work?
    - Consistent hashing is a technique that maps both servers and content objects to the same ID space. It assigns an object to its sucessor server on that circle.

- Why would a centralized design with a single DNS server not work?
    - Single point of failure
    - Query volume
    - Pefformance delay
    - Maintenance issues

- What are the main steps that a host takes to use DNS?
    - The user's application passes the hostname to the client side of the DNS application
    - The DNS client sends a query containing the hostname
    - The DNS client receives a reply which includes the IP address for the hostname.
    - The host then initiates a TCP connection to the server

- What are the services offered by DNS, apart from hostname resolution?
    - Mail server/Host aliasing
    - Load distribution

- What is the structure of the DNS hierarchy? Why does DNS use a hierarchical scheme?
    - DNS hierarchy:
        - Root DNS servers
        - Top level domain (TLD) servers
        - Authoritative servers
        - Local DNS servers
    - DNS uses this hierarchical scheme to solve the scalability problem of a centralized system

- What is the difference between iterative and recursive DNS queries?
    - In an iterative query, the querying host or server is referred to a different DNS server in the chain and must the query that next server itself
    - In a recursive query, the querying host or server delegates the query to the next DNS server, meaning that the next server is responsible for finding the answer and returning the final result to the previous server or host.

- What is DNS caching?
    - After reciving a hostname-to-IP address mapping response, a DNS server stores that information in its cache memory.

- What is a DNS resource record?
    - It is a data structure, contained inside DNS reply messages, that stores the mapping between hostnames and IP addresses.
    - It has four fields: the name, value, Type, and TTL

- What are the most common types of resource records?
    - TYPE A
    - TYPE NS
    - TYPE CNAME
    - TYME MX

- Describe the DNS message format.
    - The DNS message format consists of six main sections:
        - ID
        - Flags
        - Question
        - Answer
        - Authority
        - Additional

- What is IP Anycast?
    - IP Anycast is a network protocol strategy that routes a client to the closest server as determined by the BGP protocol. It achieves this by assigning the same IP address to multiple servers in different locations and then BGP routes select the route corresponding to the shortest path to that shared IP address.

- What is HTTP Redirection?
    - HTTP Redirection is a protocll that works at the HTTP-layer where a server (server A), upon receiving a client's GET request, can redirect the client to a different server (server B). It does this by sending an HTTP request with a code 3xx and the name of the new server.