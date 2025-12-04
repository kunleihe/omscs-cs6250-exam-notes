# Lesson 7: SDN (Part 1)

- What spurred the development of Software Defined Networking (SDN)?
    - Diversity of equipment
    - Proprietary technologies

- What are the three phases in the history of SDN?
    - Active networks
    - Control and data plane separation
    - OpenFlow API and network operating systems

- Summarize each phase in the history of SDN.
    - Active networks (Mid-1990s to Early 2000s)
        - A clean slate approach focused on **data plane programmability**. Driven by slow protocol standardization, it aimed to open network controll by allowing end-users to inject custom code into network nodes to customize functionality. This was achieved through two models: the capsule model (code in data packets) and the programmable router model (out-of-band code). Key contribution was introducing the idea of a programmable network.
    - Control and data plane separation (2001-2007)
        - The goal was to solve immediate problems for network operators (ISPs) like better traffic engineering and easier network management.
    - OpenFlow API and network operating systems (2007 to 2010)
        - This phase led to the first widespread deployment of the SDN concept. OpenFlow was an open, standardized protocol that defined the interface between the control and data plane. It generalizing network devices, promoting the vision of a Network Operating System, and solidifying distributed state management techniques.

- What is the function of the control and data planes?
    - Control plane: routing
    - Data plane: forwarding

- Why separate the control from the data plane?
    - Independent evolution and development
    - Control from high-level software program

- Why did the SDN lead to opportunities in various areas such as data centers, routing, enterprise networks, and research networks?
    - Data centers
        - Large data centers have thousands of severs and VMs. SDN makes the network management easier.
    - Routing
        - SDN makes it easier to update the router's state and provide mores control over path selection.
    - Enterprise networks
        - SDN improves the security applications for enterprise network. For example, SDN makes it easier to protect a network from DDoS attack.
    - Research networks
        - SDN allows research networks to coexist with production networks.

- What is the relationship between forwarding and routing?
    - Forwarding is a local function for routers that takes place in nanoseconds and is implemented in the hardware. It is a function of the data plane.
    - Routing is determining the path from the sender to the receiver across the network. It relies on the routing algorithms. It is the function of the control plane.

- What is the difference between a traditional and SDN approach in terms of coupling of control and data plane?
    - In traditional appraoch, the router is responsible for both routing and forwarding. In other words, the control plane (routing) and the data plane (forwarding) are closely related.
    - In the SDN approach, the router is only responsible for forwarding. The remote controller is responsible for routing (the control plane function, i.e., computing and distributing the forwarding table).

- What are the main components of an SDN network and their responsibilities?
    - The SDN-controlled network elements
        - These are the ctual networking devices like switches and routers that live in the data plane. They forward traffic in nanoseconds.
    - SDN controller
        - A logically centralized entity that act as the interface between the network elements and the network-control applications
    - Network-control applications
        - Programs that run on top of the controller, living in the control plane. They are the high-level intelligence that decides the network's overall policy. They use the network information provided by the SDN controller to make decisions about things such as routing, access control, and load balancing.

- What are the four defining features of an SDN architecture?
    - Flow-based forwarding
        - The rules for forwarding packets can be computed on any number of header field values in various layers such as the transport layer, network layer, and link layer.
    - Separation of data plane and control plane
    - Network control functions
        - The SDN control plane consists of two components: the controller and the network applications. The controller maintains up-to-date network state information about network devices and provides it to the network-control applications, which in turn use the information to monitor and control network devices.
    - A programmable network

- What are the three layers of SDN controllers?
    - Communication layer
        - This layer contains a protocol for communication between the SDN controller and the network controlled elements. This is known as the **southbound** interface. One example is OpenFlow.
    - Network-wide state-management layer
        - The network-state maintained by the SDN controller. The network-state includes information about the state of the hosts, links, switches, and other controlled elements. It also has copies of the flow tables of the switches.
    - Interface to the network-control application layer
        - The controller's **northbound** interface for the interaction between the SDN controller and the network-control applications.