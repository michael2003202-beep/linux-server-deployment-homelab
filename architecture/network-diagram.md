MacBook (Host Machine)
│
│  SSH → localhost:2222
│  HTTP → localhost:8080
│
└── VirtualBox NAT Network
      │
      └── Ubuntu Server VM
            │
            ├── NGINX Web Server (Port 80)
            └── MySQL Database