# Proxy Exit Node

## Environment

- Debian 12

## Setup

1. IP Quality Test
    ```bash
    bash <(curl -Ls IP.Check.Place) -f
    ```

2. Install X-UI [https://github.com/MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui)
    ```bash
    bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
    ```
  1. Configure `443` as Listening Port

3. HTTPS: `x-ui` >> Select `Cloudflare SSL Certificate` (*Use default 80 port)

   Optional: remove cercitificate:

    ```bash
    ~/.acme.sh/acme.sh --remove -d <domain_name> --ecc
    rm -r /root/.acme.sh/<domain_name>_ecc/
    rm -r ~/cert/<domain_name>/
    ```

   Optional: if failed, use Cloudflare SSL Certificate

4. Add Inbound: Edit Client, Enable Sniffing

## Problems

listen tcp 127.0.0.1:62789: bind: cannot assign requested address

```bash
ip addr add 127.0.0.1/8 dev lo
ip link set lo up
```
