# Lesson 10: Internet Surveillance and Censorship
- What is DNS censorship?
    - DNS censorship is a large-scale network traffic filtering strategy used by a network to enforce control and censorship over the Internet infrastructure. The purpose is to block access to specific domain names. Example: the Greate Firewall of China

- What are the properties of GFW (Great Firewall of China)?
    - Locality of GFW nodes
    - Centralized management
    - Load balancing

- How does DNS injection work?
    - For blocked DNS requests by the GFW, the GFW will respond with a fake DNS record to prevent the client from reaching the requested content.

- What are the three steps involved in DNS injection?
    1. A DNS probe is sent to the open DNS resolvers
    2. The GFW checks the probe against a blocklist
    3. If the domain is on the blocklist, a fake DNS A record response is sent back to the user instead a legitimate one, thus blocking access.

- List five DNS censorship techniques and briefly describe their working principles.
    - Packet dropping
        - The censor drops all network traffic to undesirable IP addresses
    - DNS poisoning
        - When a DNS query to resolve a hostname is received, the censor sends no answer or an incorrect answer back to the user, preventing the user from reaching the intended website.
    - Content Inspection
        - Network traffic is examined for objectionable content, proxy-based or IDS-based
    - Blocking with resets
        - The censor actively blocks individual connections containing requests with objectionable content by sending a TCP reset packet to the client, which immediately terminates the connection
    - Immediate rest of connections
        - After a user sends a requests containing flaggable keywords, the system suspends traffic from that source for a period of time. The system sends a TCP reset packet immediately upon receiving any subsequent connection attempt from that source, regardless of the new request's content.

- Which DNS censorship technique is susceptible to overblocking?
    - Packet dropping. Overblocking occurs when two websites share the same IP address.

- What are the strengths and weaknesses of the “packet dropping” DNS censorship technique?
    - Strengths: easy to implement, low cost
    - Weaknesses: maintenance of blocklist, overblocking

- What are the strengths and weaknesses of the “DNS poisoning” DNS censorship technique?
    - Strengths: no overblocking
    - Weaknesses: blocks the entire domain, not possible to allow specific services while blocking other parts of the domain

- What are the strengths and weaknesses of the “content inspection” DNS censorship technique?
    - Strengths: precise censorship, flexible
    - Weaknesses: not scalable (proxy-based)

- What are the strengths and weaknesses of the “blocking with resets” DNS censorship technique?
    - Not provided

- What are the strengths and weaknesses of the “immediate reset of connections” DNS censorship technique?
    - Not provided

- Our understanding of censorship around the world is relatively limited. Why is it the case? What are the challenges?
    - Diverse management
    - Need for scale
    - Identifying the intent to restrict content access
    - Ethics and minimizing risks

- What are the limitations of main censorship detection systems?
    - They are either no longer in use or rely on volunteer effort which makes it hard to make continuous and diverse measurements.

- What kind of disruptions does Augur focus on identifying?
    - Augur focuses on identifying IP-based distruptions as opposed to DNS-based manipulations.

- How does Iris counter the issue of lack of diversity while studying DNS manipulation? What are the steps associated with the proposed process?
    - It uses open DNS resolvers located all over the globe
    - Process:
        - Scanning the Internet's IPv4 space for open DNS resolvers
        - Identifying infrastructure DNS resolvers

- What are the steps involved in the global measurement process using DNS resolvers?
    - Perform global DNS queries
    - Annotate DNS responses with auxiliary information
    - Additional PTR and TLS scanning

- What metrics does Iris use to identify DNS manipulation once data annotation is complete?

Describe the metrics. Under what condition do we declare the response as being manipulated?
    - Consistency metrics
    - Independent verifiability metrics
    - If neither is satisfied, the response is said to be manipulated

- How to identify DNS manipulation via machine learning with Iris?
    - Not provided.

- How is it possible to achieve connectivity disruption using the routing disruption approach?
    - Withdraw advertised BGP network prefixes or re-advertise them with altered properties

- How is it possible to achieve connectivity disruption using the packet filtering approach?
    - Use firewalls and switches to block packets

- Explain a scenario of connectivity disruption detection in the case when no filtering occurs.
    - Detections relies on IP ID counter incrementing by 2. If the measurement machine sees an increase of 2, it means the two hosts communicated

- Explain a scenario of connectivity disruption detection in the case of inbound blocking.
    - Traffic from the reflector to the site with objectionable data is blocked, thus the IP ID only increases by 1.

- Explain a scenario of connectivity disruption detection in the case of outbound blocking. 
    - Outbound reset packets from the reflector do not reach the site. The site will continue to send SYN-ACK packets until it receives an ACK, causing the reflector's IP ID to increase by 2 each time.