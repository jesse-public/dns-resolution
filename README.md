# dns-resolver
PiHole + Unbound DNS in Docker

## Example `docker-compose.yml`

```yml
version: "3"

volumes:
  pihole:
  dnsmasq:

services:
  dns:
    container_name: dns-resolver
    image: dns-resolver
    hostname: ${HOSTNAME}
    domainname: ${DOMAINNAME}
    ports:
      - 443:443/tcp
      - 80:80/tcp
      - 53:53/tcp
      - 53:53/udp
    environment:
      ServerIP: ${SERVERIP}
      TZ: ${TZ}
      WEBPASSWORD: ${WEBPASSWORD}
      REV_SERVER: ${REV_SERVER}
      REV_SERVER_TARGET: ${REV_SERVER_TARGET}
      REV_SERVER_DOMAIN: ${REV_SERVER_DOMAIN}
      REV_SERVER_CIDR: ${REV_SERVER_CIDR}
      PIHOLE_DNS_: 127.0.0.1#5335;127.0.0.1#5335
      DNSSEC: "true"
    volumes:
      - pihole:/etc/pihole:rw
      - dnsmasq:/etc/dnsmasq.d:rw
    restart: unless-stopped
    ```
    