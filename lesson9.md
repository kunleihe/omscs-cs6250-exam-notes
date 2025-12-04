# Lesson 9: Internet Security
- What are the properties of secure communication?
    - Confidentiality: message is only available to the sender and the receiver
    - Integrity: message has not been modified while in transit
    - Authentication: the sender and the receiver are who they say they are
    - Availability: the information is available

- How does Round Robin DNS (RRDNS) work?
    - It distributes the load of incoming requests to serveral severs at a single physical location. It responds to a DNS requests with a list of DNS A records, which it then cycles in a round-robin manner.

- How does DNS-based content delivery work?
    - When a lookup is conducted for a content, the delivery network will determine the best CDN server (the nearest server) to service the request and use DNS to point the colient to the right IP address.

- How do Fast-Flux Service Networks work?
    - It is based on a rapid change in DNS answers, with a TTL lower than that of RRDNS and CDN, in order to prevent spammers for injecting bad IP address.

- What are the main data sources used by FIRE (FInding Rogue nEtworks) to identify hosts that likely belong to rogue networks?
    - Botnet command and control providers
    - Drive-by-download hosting providers
    - Phish housing providers

- The design of ASwatch is based on monitoring global BGP routing activity to learn the control plane behavior of a network. Describe 2 phases of this system.
    - Training phase: ASwatch learns features of malicious and legitimate ASes
    - Operational phase: determine if an AS is malicious

- What are 3 classes of features used to determine the likelihood of a security breach within an organization?
    - Mismanagement symptoms
    - Malicious Activities
    - Security Indicent Reports

- (BGP hijacking) What is the classification by affected prefix?
    - It is about the IP prefixes that are advertised by BGP. There are different ways the prefix can be targeted:
        - exact prefix hijacking
        - sub-prefix hijacking
        - squatting.

- (BGP hijacking) What is the classification by AS-Path announcement?
    - An illegitimate AS announces the AS-path for a prefix for which it doesn't have ownership rights. There are different ways this can be achieved: 
        - type-0 hijacking
        - type-N hijacking
        - type-U hijacking

- (BGP hijacking) What is the classification by data plane traffic manipulation?
    - To hijack the network traffic and maniulate the redirected network traffic on its way to the receiving AS. Three ways the attack and be realized: traffic intercepted by the hijacker can be 
        - dropped (blackholing attack)
        - eavesdropped or manipulated (man-in-the-middle attack)
        - impersonated (imposture attack)

- What are the causes or motivations behind BGP attacks?
    - Human error, targeted attack, high impact attack

- Explain the scenario of prefix hijacking.
    - Malicious AS router advertises a prefix that it doesn't own, using its shorter distance to have peer/customer routers change their path for the prefix to the malicious AS.

- Explain the scenario of hijacking a path.
    - Malicious AS receives a path and alters it, placing itself as the best path to reach an AS. This path is shorter than the original one, causing other ASes to use the new hijacked path.

- What are the key ideas behind ARTEMIS?
    - A configuration file where all the prefixes owned by the network are listed for reference
    - A mechanism for receiving BGP updates which allows receiving updates from local routers and monitoring servies.

- What are the two automated techniques used by ARTEMIS to protect against BGP hijacking?
    - Prefix deaggregation: annoucing more specific prefixes
    - Mitigation with Multiple Origins: third party orgs and service providers do BGP announcements for a given network

- What are two findings from ARTEMIS?
    - Outsourcing the task of BGP announcement to third parties is highly effective
    - Outsourcing BGP announcements is more optimal than prefix filtering

- Explain the structure of a DDoS attack.
    - An attempt to compromise a server or network resources with a flood of traffic
    - To achieve this, the attacker first compromises and deploys flooing servers (slaves).
    - Later when initiating an attack, the attacker instructs these flooding servers to send a high volumne of traffic to the victim.

- What is spoofing, and how is related to a DDoS attack?
    - Setting a false IP address in the source field of a packet to impersonate a legitimate server. 
    - In one form, the source IP address is spoofed, so the response of the server is sent to some other client instead of the attacker's machine
    - In the other form, the attacker sets the same IP address in both the source and the destination ID fields, resulting in the server sending the replies to itself, causing it to crash.

- Describe a Reflection and Amplification attack.
    - An attacker master commands a set of slaves to send requests to a very large number of reflectors. 
        - Spoofing: The slaves spoof the source IP address of these requests, setting it to the victim's IP.
        - Reflection: The reflectors send their responses back to the victim's IP, reflecting millions of response packets to the victim.
        - Amplification: The reflectors send large responses to the victim, exhausting the victim's bandwidth and wasting its resources so that it cannot handle legitimate requests.

- What are the defenses against DDoS attacks?
    - Traffic scrubbing services: diverts the incoming traffic to a specialized server and separates the bad traffic from the clean traffic, and only forward the clean traffic
    - ACL filters: filters out unwanted traffic at AS border routers
    - BGP flowspec: allows network to create and progagate fine-grained rules across their border routers to match traffic flows and take actions

- Explain provider-based blackholing.
    - Provider-based BGP blackholing is a technique to stop high-volume DDoS attack traffic closer to the source by dropping it to a null location.
    - The victim AS annouces the specific attacked host IP prefix to its upstream provider via BGP
    - The BGP message must include the provider's specific blackhole community attribute
    - The provider identifies the message, sets the next-hop for that prefix to a blackholing IP and drops all incoming traffic intended for the victim host.

- Explain IXP blackholing.
    - The victim AS sends a BGP blackholing message to the IXP route server
    - The route server identifies the message, sets the next-hop for the attacked IP to a blackholing IP and propagates this announcements to all connected IXP member ASes.
    - All member ASes drop the traffic intended for the victim host at their own borders

- What is one of the major drawbacks of BGP blackholing?
    - The destination under attach becomes unreachable because all traffic, including the legitmate traffic, is dropped.