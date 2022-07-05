# docker-tor

Docker Setup of local Tor Proxy for remote SSH access.

## Status

Tor Version: `0.4.7.8`

Work in progress. Not yet tested.

> last updated: 2022-07-05

## Resources

- <https://github.com/lncm/docker-tor>
- <https://github.com/blckbx/ssh_over_tor>

### Windows SSH Client over Tor specific

- <https://forum.blocktrainer.de/t/homeserver-ssh-zugriff-ueber-tor-hidden-service/51>
- <https://stackoverflow.com/questions/71335954/how-to-ssh-with-keys-from-windows-10-to-remote-service-behind-tor-onion-address>
- <https://stackoverflow.com/questions/36865665/open-putty-ssh-connection-over-socks5-proxy-via-command-line?rq=1>
- <https://stackoverflow.com/questions/67320844/how-open-ssh-can-connect-through-socks5-proxy-on-windows-putty-is-not-an-option?rq=1>
- <https://www.reddit.com/r/TOR/comments/mou6ks/question_re_tortorifytorsocks_and_windows_os/>
- <https://github.com/3ndG4me/socat/releases>

## Tor Setup on Linux Server

> tbd.

## SSH Setup on Client Side

### Checking Tor Connection

- _Pifall 1_: Tor Browser on Windows has different port for **socks5** proxy:
  - Port `9150` for the Tor Browser.
  - If you install the Tor deamon on Windows, it still should be port `9050` if the default settings haven't been altered.
- _Pifall 2_: You need `curl` with `socks5` proxy support.
  - On Windows you can use `cmder` shell.
    - <https://cmder.net/>

```sh
curl https://check.torproject.org/api/ip
{"IsTor":false,"IP":"49.30.XX.XX"}
```

```sh
curl --socks5 127.0.0.1:9050 https://check.torproject.org/api/ip
{"IsTor":true,"IP":"185.220.XXX.XXX"}
```

## Linux SSH Client over Tor Setup

## Windows SSH Client over Tor Setup
