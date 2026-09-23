# day5-networking 
Q1. What is a Port? Explain with a real-world example.
A Port is a logical communication endpoint on an operating system used by services and applications to receive and transmit network traffic.
 * Real-World Example: Consider a server as an apartment building. The building's street address represents the IP Address. Each apartment's door number represents a Port, and the resident living inside that apartment is the Service. A visitor arriving at Room 80 interacts with the Web Server, while someone knocking on Room 22 interacts with SSH.
Q2. Differentiate between an IP Address and a Port.
 * IP Address: Identifies the device/host on the network (IP identifies the device).
 * Port: Identifies the specific application or process running on that device (Port identifies the service).
Q3. A server has the IP address 54.234.xxx.xxx. How does the server identify whether a request is for Website, SSH, Database, or Email? Explain.
The server examines the destination port number specified in the incoming packet header:
 * Packets sent to Port 80 / 443 are routed to the Web Server process.
 * Packets sent to Port 22 are directed to the SSH daemon.
 * Packets targeting Port 3306 / 27017 are forwarded to MySQL or MongoDB engines.
 * Packets sent to Port 25 are handed over to the SMTP mail service.
Q4. Write the port numbers used by SSH, DNS, HTTP, HTTPS, MySQL, PostgreSQL, MongoDB, Redis, and Jenkins.
 * SSH: 22
 * DNS: 53
 * HTTP: 80
 * HTTPS: 443
 * MySQL: 3306
 * PostgreSQL: 5432
 * MongoDB: 27017
 * Redis: 6379
 * Jenkins: 8080
Q5. Differentiate between TCP and UDP. Include definition, characteristics, and examples.
 * TCP (Transmission Control Protocol):
   * Definition: A connection-oriented transport protocol that guarantees ordered and reliable packet delivery.
   * Characteristics: Reliable, uses a 3-way handshake (SYN \rightarrow SYN-ACK \rightarrow ACK), error-checked, sequence-tracked.
   * Examples: Web browsing (HTTP/HTTPS), SSH, file transfers.
 * UDP (User Datagram Protocol):
   * Definition: A connectionless, lightweight transport protocol designed for rapid transmission without delivery confirmation.
   * Characteristics: Fast, no handshake overhead, fire-and-forget, stateless.
   * Examples: DNS queries, live video streaming, multiplayer gaming.
Q6. Why does HTTP use TCP instead of UDP?
HTTP powers the delivery of web pages consisting of HTML, CSS, JavaScript, and data payloads. A single dropped or unordered packet could corrupt code execution or page rendering. TCP's reliability, automated retransmissions, and packet sequencing ensure error-free data delivery.
Q7. DNS commonly uses which protocol? Explain why.
 * Protocol: UDP
 * Reason: DNS lookups involve simple, lightweight single-packet requests and replies. Using UDP eliminates the latency associated with the 3-way TCP handshake, allowing near-instant domain name resolution.
Q8. What is a Firewall? Explain using a real-world analogy.
A Firewall is a network security system that monitors, filters, and controls incoming and outgoing network traffic based on configured security rules.
 * Analogy: It acts like a Security Guard stationed at an entrance gate. The guard verifies visitors' IDs against an access list, allowing approved guests inside while rejecting unauthorized or suspicious individuals.
Q9. How does a Firewall improve server security?
 * It closes vulnerable and unnecessary network ports, preventing malicious access to internal services.
 * It prevents port scanning, unauthorized intrusions, and blocks unwanted or hostile traffic from the public Internet.
Q10. Differentiate between Inbound Rules and Outbound Rules with examples.
 * Inbound Rules: Control and filter traffic coming INTO the server from external sources.
   * Example: Allowing external web traffic on ports 80/443 or SSH access on port 22.
 * Outbound Rules: Control and filter traffic going OUT from the server to external networks.
   * Example: Allowing the server to contact an external endpoint like Google APIs or OS package mirrors to pull updates.
Q11. What is an AWS Security Group? Why is it called a Cloud Firewall?
An AWS Security Group is a virtual, stateful firewall that controls inbound and outbound network traffic at the instance level (e.g., for EC2 instances). It is referred to as a cloud firewall because it operates virtually within AWS cloud hypervisors rather than on dedicated physical hardware appliances.
Q12. A web server should be accessible over the Internet. Which ports should be allowed through the firewall and why?
 * Port 80 (HTTP): Allowed for standard unencrypted web requests and HTTP-to-HTTPS redirects.
 * Port 443 (HTTPS): Allowed for TLS/SSL-encrypted secure public web traffic.
 * Port 22 (SSH): Allowed (ideally restricted to trusted IPs) to permit secure remote administration by engineers.
Q13. Why should database ports such as MySQL (3306) and MongoDB (27017) not be publicly accessible?
Databases hold sensitive application and user information. Opening these ports to the Internet invites automated credential attacks, exploit scans, and unauthorized data exfiltration. They should strictly accept internal connections from application runtimes within an isolated local network.
Q14. Expand NAT. What problem does NAT solve?
 * Expansion: Network Address Translation.
 * Problem Solved: Solves the global shortage and exhaustion of IPv4 addresses by allowing multiple internal hosts with private IPs to share one public IP.
Q15. Write the three private IP ranges used in networking.
 * Class A: 10.0.0.0 – 10.255.255.255
 * Class B: 172.16.0.0 – 172.31.255.255
 * Class C: 192.168.0.0 – 192.168.255.255
Q16. Explain the complete NAT flow when a laptop accesses a website on the Internet.
 * The laptop initiates an outbound request using its local private IP (e.g., 192.168.1.10).
 * The packet reaches the local router/NAT gateway.
 * The NAT device rewrites the source header, swapping the private IP with its public IP (e.g., 203.0.113.5) and logs this in a translation table.
 * The destination server replies to the public IP. The NAT router references its table and forwards the incoming response to the laptop's private IP.
Q17. What are the advantages of NAT?
 * Saves Public IP addresses: Conserves scarce IPv4 addresses by multiplexing private devices through one address.
 * Hides Internal Network: Obscures private topology, IP assignments, and infrastructure from external observers.
 * Improves Security: Blocks unsolicited external inbound connections from directly reaching client machines.
Q18. Expand VPN. What is the purpose of a VPN?
 * Expansion: Virtual Private Network.
 * Purpose: To provide an encrypted and private communication tunnel over an unsecure public network (like the Internet).
Q19. Explain how a VPN creates secure communication between a user and a company network.
The user runs a VPN Client that establishes an encrypted tunnel with a remote VPN Server. All outbound and inbound data packets are encapsulated and encrypted within this tunnel. Intermediaries, such as ISPs and network eavesdroppers, cannot read packet contents or determine real traffic destinations.
Q20. List four benefits of using a VPN.
 * Encrypts Traffic: Ensures confidentiality across open or untrusted networks.
 * Secure Remote Access: Enables off-site workers to safely access internal corporate networks.
 * Protects Data: Prevents packet sniffing, data tampering, and identity exposure.
 * Connects to Private Networks: Joins remote hosts into internal office/cloud VPC environments.
Q21. Name any four VPN solutions used in real-world environments.
 * OpenVPN
 * WireGuard
 * AWS Client VPN
 * Cisco AnyConnect
Q26. Compare your private IP and public IP. Are they the same? Why are they different? Which networking concept is responsible?
 * Comparison: They are not the same (Private IP ≠ Public IP).
   * Private IP: 172.19.160.92 (bound locally to the interface).
   * Public IP: Visible via curl ifconfig.me (represents the external gateway on the Internet).
 * Why they are different: A private IP is non-routable over the public Internet and only works locally. Accessing public resources requires mapping internal traffic to a routable public IP.
 * Responsible Concept: NAT (Network Address Translation).
Q27. Production Scenario: Users need secure website access, developers need SSH access, and the database must remain private. Which ports should be open, blocked, and what firewall rules would you configure?
 * Open Ports (Allowed Inbound):
   * Port 443 (HTTPS): Open to 0.0.0.0/0 for encrypted public web access.
   * Port 80 (HTTP): Open to 0.0.0.0/0 to redirect traffic to HTTPS.
   * Port 22 (SSH): Open strictly to the specific IP addresses or VPN network of developers/administrators.
 * Blocked Ports (Denied Inbound):
   * Ports 3306 (MySQL) & 27017 (MongoDB): Strictly blocked from public Internet access ("Database should not be public").
 * Firewall Rules Configuration:
   * Configure a default-deny inbound firewall policy.
   * Allow inbound on ports 80 and 443 from any source.
   * Allow inbound on port 22 exclusively from developer IPs.
   * Restrict database ports to receive connections only from application containers or internal subnets.
Q28. Explain the production flow: User → Internet → Firewall → Load Balancer → Nginx → Docker Container → Database.
 * User: Enters a URL into the browser, triggering an HTTP/HTTPS request.
 * Internet: Transmits data packets across public networks toward the hosting infrastructure.
 * Firewall: Evaluates incoming packets, dropping unauthorized connection attempts and passing valid traffic on open ports.
 * Load Balancer: Receives legitimate traffic, offloads SSL/TLS encryption, and balances incoming requests evenly across healthy backend instances.
 * Nginx: Acts as an internal reverse proxy, handling URL rewrites and forwarding requests to the respective application service.
 * Docker Container: Executes the backend application codebase and processes the business logic.
 * Database: Receives internal database queries from the container, processes the request, and returns data securely without public network exposure.
