# dns-resolution
PiHole + Unbound DNS in Docker

## Example `docker-compose.yml`

```yml
version: "3"

volumes:
  pihole:
  dnsmasq:

services:
  dns:
    ulimits:
      nofile:
        soft: 1024
        hard: 4096
    container_name: dns-resolution
    image: dns-resolution
    hostname: ${HOSTNAME}
    domainname: ${DOMAINNAME}
    ports:
      - 443:443/tcp
      - 53:53/tcp
      - 53:53/udp
    environment:
      ServerIP: ${SERVERIP}
      TZ: ${TZ}
      WEBPASSWORD: ${WEBPASSWORD}
      WEBTHEME: "default-dark"
      PIHOLE_DNS_: 127.0.0.1#5335;127.0.0.1#5335
      DNSSEC: "false" # unbound will perform DNSSEC
    volumes:
      - pihole:/etc/pihole:rw
      - dnsmasq:/etc/dnsmasq.d:rw
      - ./volumes/pihole-certs:/etc/pihole-certs
    restart: unless-stopped
```
    
## Example `.env`

```
HOSTNAME=dns-resolution
DOMAINNAME=local
SERVERIP=192.168.0.2
TZ=America/Los_Angeles
WEBPASSWORD=supersecretpasswordgoeshere!
```
