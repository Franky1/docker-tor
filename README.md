# docker-tor

Docker Setup of local Tor Proxy for remote SSH access.

## Resources

- <https://github.com/lncm/docker-tor>
- <https://github.com/3ndG4me/socat/releases>

## Tor Setup

> tbd.

## Checking Tor

> Caveat: Tor Browser on Windows has different ports for socks5 Proxy: 9150, 9151.

```sh
curl https://check.torproject.org/api/ip
{"IsTor":false,"IP":"49.30.XX.XX"}
```

```sh
curl --socks5 127.0.0.1:9050 https://check.torproject.org/api/ip
{"IsTor":true,"IP":"185.220.XXX.XXX"}
```

## Client Windows SSH Setup
