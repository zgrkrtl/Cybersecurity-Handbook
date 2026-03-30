# Proxy Servers

## What is a Proxy Server?

A **proxy server** is hardware or software that acts as a **gateway between a client and a server**, used for many different purposes depending on the need.

---

## Types of Proxy Servers

### Forward Proxy Server
The most widely used proxy type. Directs requests from a **private network to the internet** through a firewall.

### Transparent Proxy Server
Forwards requests and responses to the target **without modifying** any incoming or outgoing traffic.

### Anonymous Proxy Server
Enables **anonymous browsing** on the internet by masking the client's identity.

### High Anonymity Proxy Server
Takes anonymity further — does **not send proxy type or client IP** in the request, making the client very difficult to track.

### Distorting Proxy Server
Hides its identity by **posing as a website's proxy**. Changes the real IP address to protect client confidentiality.

### Data Center Proxy Server
Not connected to an ISP — instead gets service through **data centers**. Fast response times but **insufficient anonymity**.

### Residential Proxy Server
Passes all client requests through a residential IP. Can **block unwanted/suspicious ads** and is considered more secure than most other proxy types.

### Public Proxy Server
A **free proxy available to everyone**. Good for cost-free use but sacrifices both **security and speed** since it's open to all.

### Shared Proxy Server
Used by **multiple people simultaneously**. Fast and cost-effective, but one user's activity can affect others — for example, if one user gets the IP blocked, everyone using it loses access to that server.

### SSL Proxy Server
Provides **bidirectional encrypted communication** between client and server. Considered secure due to encryption against threats.

### Rotating Proxy Server
Assigns a **separate IP address to each client**, making tracking significantly harder.

### Reverse Proxy Server
Sits in front of servers — **validates and processes requests** so the client never communicates directly with the backend. Popular examples: **Varnish** and **Squid**.

### Split Proxy Server
Runs as **two programs on two separate computers**, splitting the proxy workload.

### Non-Transparent Proxy Server
Sends all requests through a **firewall**. Clients using it are aware their traffic is going through the firewall.

### Hostile Proxy Server
Used maliciously to **eavesdrop on traffic** between a client and a target. A tool for interception and surveillance.

### Intercepting Proxy Server
Combines both **proxy server features and gateway features** together.

### Forced Proxy Server
Applies **both blocking and allowing policies** simultaneously.

### Caching Proxy Server
Has a built-in **caching mechanism** — serves cached responses to clients instead of fetching fresh data every time.

### Web Proxy Server
Operates specifically on **web traffic**.

### SOCKS Proxy Server
Prevents external network components from **obtaining information about the client**, offering a deeper layer of privacy.

### HTTP Proxy Server
A proxy with a **caching mechanism specifically for HTTP protocol**.


---
*Documentation structured and formatted with the assistance of generative AI.*
