```bash
Host Machine (MacBook)
        │
        │
        ▼
VirtualBox NAT Network
        │
        │  localhost:2222 → SSH
        │  localhost:8080 → HTTP
        │
        ▼
Ubuntu Server VM
        │
        ├─ NGINX Web Server
        │
        └─ MySQL Database
```