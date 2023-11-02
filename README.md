# enum_scan
Scan d'énumération de cibles

# Énumération du réseau
```bash
ping $IP #63 ttl = linux #127 ttl = windows
```

```bash
nmap -p- --min-rate 1000 $IP
nmap -p- --min-rate 1000 $IP -Pn #désactive la commande ping et analyse uniquement les ports
```

```bash
nmap -p <ports> -sV -sC -A $IP
```

# Stealth Scan
```bash
nmap -sS -p- --min-rate=1000 10.11.1.229 -Pn #stealth scans
```
