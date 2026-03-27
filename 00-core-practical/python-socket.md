# Python Socket Examples


## 1. Simple TCP Client 

Connect to a server, send data, receive a response.

```python
import socket

sck = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sck.connect(("example.com", 80))
sck.send(b"GET / HTTP/1.0\r\nHost: example.com\r\n\r\n")
response = sck.recv(4096)
sck.close()

```


---

## 2. TCP Server

A server that listens for connections and echoes back whatever the client sends.

```python
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind(("127.0.0.1", 9999))
server.listen(5)

while True:
    client_socket, client_address = server.accept()
    print(f"Connection from {client_address}")

    data = client_socket.recv(1024)
    print(f"Received: {data.decode()}")

    client_socket.send(b"Echo: " + data)
    client_socket.close()
```

How servers work bind a port, listen, accept connections one by one.

---

## 3. UDP Client and Server

```python
import socket
# --- SERVER SIDE ---

server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
server.bind(("127.0.0.1", 9998))
print("UDP server listening...")

data, sender_address = server.recvfrom(1024)
print(f"Got from {sender_address}: {data.decode()}")

server.sendto(b"Got your message", sender_address)
server.close()
```

```python
import socket

# --- CLIENT SIDE ---
client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

client.sendto(b"Hello UDP server", ("127.0.0.1", 9998))

data, server_address = client.recvfrom(1024)
print(f"Server replied: {data.decode()}")

client.close()
```

---

## 4. Port Scanner 

Uses `connect_ex()` instead of `connect()` returns an error code instead of raising an exception.

```python
import socket

target = "127.0.0.1"
open_ports = []

print(f"Scanning {target}...")

for port in range(1, 1025):
    sck = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    sck.settimeout(0.5)
    result = sck.connect_ex((target, port))

    if result == 0:
        open_ports.append(port)
        print(f"Port {port} is OPEN")

    sck.close()

print(f"\nScan complete. Open ports: {open_ports}")
```

---

## 5. IPv6 TCP Client

```python
import socket

sck = socket.socket(socket.AF_INET6, socket.SOCK_STREAM)

sck.connect(("2606:2800:21f:cb07:6820:80da:af6b:8b2c", 80, 0, 0))

sck.send(b"GET / HTTP/1.0\r\nHost: example.com\r\n\r\n")

response = sck.recv(4096)
print(response.decode())

sck.close()
```

---

## Quick Reference

| Parameter | Meaning |
|-----------|---------|
| `AF_INET` | Use IPv4 |
| `AF_INET6` | Use IPv6 |
| `SOCK_STREAM` | Use TCP |
| `SOCK_DGRAM` | Use UDP |
| `connect()` | Raises exception on failure |
| `connect_ex()` | Returns error code on failure |
| `bind()` | Claim a port (servers) |
| `listen()` | Start accepting connections |
| `accept()` | Wait for a client to connect |
| `send()` / `recv()` | TCP send and receive |
| `sendto()` / `recvfrom()` | UDP send and receive (no connection needed) |
| `settimeout(n)` | Give up after n seconds |
| `close()` | Release the socket and port |


---
*Documentation structured and formatted with the assistance of generative AI.*
