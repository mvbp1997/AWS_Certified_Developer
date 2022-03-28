## Exploring Elastic Load Balancers
A load balancer distributes network traffic across a group of servers; can easily increase capacity when needed
- Application Load Balancer: HTTP and HTTPS
- Network Load Balancer: TCP and high performance
- Classic Load Balancer: HTTP/HTTPS and TCP (legacy)
- Gateway Load Balancer: allows you to load balance workloads for third-party virtual appliances running in AWS
  - virtual appliances purchased using the AWS marketplace
  - virtual firewalls from companies like Fortinet, Palo Alto, Juniper, Cisco
  - IDS/IPS systems from companies like Checkpoint, etc.

### 7 Layer Model
- conceptual framework which describes the function of a network
- layer 7: application layer - HTTP, web browsers, what end user sees
- layer 6: presentation layer - SSH, encryption, data is in usable format
- layer 5: session layer - maintain connections and sessions
- layer 4: transport - transmits data using TCP and UDP
- layer 3: network layer - logically routing network packets based on IP addresses
- layer 2: data link - physically transmits data based on MAC addresses
- layer 1: physical - transmit bits and bytes over physical devices

### Application Load Balancer
- used for load balancing HTTP/HTTPS traffic
- operate at Layer 7 and are application aware
- support advanced request routing to specific web servers based on the HTTP header
  - send the user to different servers depending on the request type

### Network Load Balancer
- used for load balancing TCP traffic where extreme performance is required
- operates at layer 4 in the Transport layer
- capable of handling millions of request per second, while maintaining low latency
- expensive

### Classic Load Balancer
- legacy option
- HTTP: support layer 7 specific features, such as X-Forwarded-For headers and sticky sessions
- TCP: also supports layer 4 load balancing

### X-Forwarded-For Header
- used to identify the originating IP address of a client connecting through a load balancer

### Common Load Balancer Errors
- Error 504: Gateway Timeout - target failed to respond
  - the Elastic Load Balancer could not establish a connection to the target
  - application could be having issues

---

## Exam Tips
- Application Load Balancers: HTTP and HTTPS; intelligent load balancing; routes requests to a specific web server based on the type of request 
- Network Load Balancers: provides high-performance load balancing for TCP only
- Classic Load Balancers: the legacy option that supports both HTTP/HTTPS and TCP
- Gateway Load Balancers: provides load balancing for third-party virtual appliances, like firewalls, IDPs, etc.
- X-Forwarded-For: if you need the IPv4 address of your end user, look for this header 

