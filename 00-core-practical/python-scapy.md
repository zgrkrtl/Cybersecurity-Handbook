# Scapy Examples

A reference guide covering common Scapy usages from basic packet building to custom protocols.

---

## 1. ICMP Ping (IPv4)

The classic ping but built by hand at the packet level.

```python
from scapy.all import IP, ICMP, sr1

pkt = IP(dst="8.8.8.8") / ICMP()
reply = sr1(pkt, timeout=2, verbose=0)

if reply:
    print(f"Reply from {reply.src} — host is alive")
else:
    print("No reply — host may be down or blocking ICMP")
```


---

## 2. ICMPv6 Ping (IPv6)

Same concept as above but for IPv6. Notice the different layer names.

```python
from scapy.all import IPv6, ICMPv6EchoRequest, ICMPv6EchoReply, sr1

pkt = IPv6(dst="2001:4860:4860::8888") / ICMPv6EchoRequest(seq=1)

reply = sr1(pkt, timeout=2, verbose=0)

if reply:
    if reply.haslayer(ICMPv6EchoReply):
        print(f"Reply from {reply.src}")
    else:
        print(f"Got unexpected response type: {reply.type}")
else:
    print("Request timed out")
```

---

## 3. ARP Scanner 

ARP works at Layer 2 (Ethernet). No IP routing needed fastest way to find hosts on your local network.

```python
from scapy.all import ARP, Ether, srp

target = "192.168.1.0/24"

pkt = Ether(dst="ff:ff:ff:ff:ff:ff") / ARP(pdst=target)

answered, unanswered = srp(pkt, timeout=3, verbose=0)

print(f"{'IP Address':<20} {'MAC Address'}")
print("-" * 40)

for sent_pkt, received_pkt in answered:
    print(f"{received_pkt[ARP].psrc:<20} {received_pkt[ARP].hwsrc}")

print(f"\n{len(answered)} hosts found, {len(unanswered)} no response")
```

---

## 4. TCP Port Scanner Using SYN Packets

Sends a SYN and checks the reply SYN-ACK means open, RST means closed. More stealthy than a full connection because the handshake never completes.

```python
from scapy.all import IP, TCP, sr1

target = "192.168.1.1"
ports = [22, 80, 443, 3306, 8080]

print(f"Scanning {target}...\n")

for port in ports:
    pkt = IP(dst=target) / TCP(dport=port, sport=12345, flags="S")

    reply = sr1(pkt, timeout=1, verbose=0)

    if reply is None:
        print(f"Port {port:5d} — FILTERED (no response)")

    elif reply.haslayer(TCP):
        tcp_flags = reply[TCP].flags

        if tcp_flags == "SA":
            from scapy.all import send
            send(IP(dst=target) / TCP(dport=port, sport=12345, flags="R"), verbose=0)
            print(f"Port {port:5d} — OPEN")

        elif tcp_flags == "RA":
            print(f"Port {port:5d} — CLOSED")
```

---

## 5. DNS Query Over UDP

Build a raw DNS question packet from scratch and read the answer.

```python
from scapy.all import IP, UDP, DNS, DNSQR, DNSRR, sr1

question = DNSQR(qname="www.example.com", qtype="A")

pkt = IP(dst="8.8.8.8") / UDP(dport=53) / DNS(rd=1, qd=question)

reply = sr1(pkt, timeout=3, verbose=0)

if reply and reply.haslayer(DNS):
    dns_reply = reply[DNS]

    print(f"Got {dns_reply.ancount} answer(s):\n")

    for i in range(dns_reply.ancount):
        record = dns_reply.an[i]

        print(f"  {record.rrname.decode()} → {record.rdata}")
else:
    print("No DNS response received")
```
---

## 6. Packet Sniffer — Capture Live Traffic

Passively listen on your network interface and inspect packets as they arrive.

```python
from scapy.all import sniff, IP, TCP, UDP, DNS

def inspect_packet(pkt):
    """Called automatically for every packet captured"""

    if pkt.haslayer(IP):
        src = pkt[IP].src
        dst = pkt[IP].dst

        if pkt.haslayer(TCP):
            sport = pkt[TCP].sport
            dport = pkt[TCP].dport
            flags = pkt[TCP].flags
            print(f"TCP  {src}:{sport} → {dst}:{dport}  flags={flags}")

        elif pkt.haslayer(UDP):
            sport = pkt[UDP].sport
            dport = pkt[UDP].dport

            if pkt.haslayer(DNS) and pkt[DNS].qr == 0:
                qname = pkt[DNS].qd.qname.decode()
                print(f"DNS  {src} asked: {qname}")
            else:
                print(f"UDP  {src}:{sport} → {dst}:{dport}")

print("Sniffing... press Ctrl+C to stop\n")
sniff(prn=inspect_packet, filter="ip", count=50, iface=None)
```

---

## 7. Custom Protocol Definition

Define your own binary protocol, then build and parse packets with it.

```python
from scapy.all import Packet, FieldLenField, StrLenField, ShortField, bind_layers, UDP

class MyProtocol(Packet):
    name = "MyProtocol"
    fields_desc = [
        ShortField("version", 1),
        FieldLenField("payload_len", None, length_of="payload"),
        StrLenField("payload", b"", length_from=lambda pkt: pkt.payload_len),
    ]

bind_layers(UDP, MyProtocol, dport=9000)

from scapy.all import IP, send

pkt = IP(dst="127.0.0.1") / UDP(dport=9000) / MyProtocol(
    version=1,
    payload=b"hello custom protocol"
)

pkt.show()

from scapy.all import Raw

raw_bytes = bytes(pkt[MyProtocol]) 
parsed = MyProtocol(raw_bytes) 
print(f"Version: {parsed.version}")
print(f"Payload: {parsed.payload}")
```

---

## Quick Reference

| Function | Description |
|----------|-------------|
| `sr1(pkt)` | Send one packet, wait for one reply |
| `sr(pkt)` | Send one packet, collect all replies |
| `srp(pkt)` | Send/receive at Layer 2 (Ethernet) |
| `send(pkt)` | Send only, don't wait for reply (Layer 3) |
| `sendp(pkt)` | Send only at Layer 2 |
| `sniff()` | Passively capture live traffic |
| `pkt.show()` | Pretty-print all packet layers and fields |
| `pkt.hexdump()` | Show raw bytes in hex |
| `pkt.haslayer(X)` | Safely check if layer X exists |
| `pkt[X]` | Access layer X (crashes if missing) |
| `pkt[X].field` | Read a specific field from layer X |

| Layer | Protocol | Common Fields |
|-------|----------|---------------|
| `Ether` | Ethernet | `src`, `dst`, `type` |
| `IP` | IPv4 | `src`, `dst`, `ttl` |
| `IPv6` | IPv6 | `src`, `dst`, `hlim` |
| `TCP` | TCP | `sport`, `dport`, `flags`, `seq`, `ack` |
| `UDP` | UDP | `sport`, `dport` |
| `ICMP` | ICMPv4 | `type`, `code`, `seq` |
| `ICMPv6EchoRequest` | ICMPv6 | `seq`, `id`, `data` |
| `ARP` | ARP | `op`, `psrc`, `pdst`, `hwsrc`, `hwdst` |
| `DNS` | DNS | `qd`, `an`, `ancount`, `rd` |
| `DNSQR` | DNS Question | `qname`, `qtype` |
| `DNSRR` | DNS Answer | `rrname`, `rdata`, `ttl` |


---
*Documentation structured and formatted with the assistance of generative AI.*