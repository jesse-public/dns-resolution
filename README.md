# dns-resolution

## Using self-signed certs

To use TLS certificates signed by a local CA:
1. copy `ca.crt` to `adguard/`
1. update compose.yml with `build: ./adguard` in place of `image: adguard/adguardhome`
