# docker-tor

Docker Setup of local TOR Proxy for remote SSH access.

## Status

Tor Version: `0.4.7.8`

Work in progress. Not everything tested yet.

> last updated: 2022-07-11

## Ressources

- <https://github.com/lncm/docker-tor>
- <https://github.com/blckbx/ssh_over_tor>
- Tutorial - SSH über Tor auf die eigene Node <https://www.youtube.com/watch?v=RhE9SomCT8k>

### Windows SSH Client over Tor specific

- <https://forum.blocktrainer.de/t/homeserver-ssh-zugriff-ueber-tor-hidden-service/51>
- <https://stackoverflow.com/questions/71335954/how-to-ssh-with-keys-from-windows-10-to-remote-service-behind-tor-onion-address>
- <https://stackoverflow.com/questions/36865665/open-putty-ssh-connection-over-socks5-proxy-via-command-line?rq=1>
- <https://stackoverflow.com/questions/67320844/how-open-ssh-can-connect-through-socks5-proxy-on-windows-putty-is-not-an-option?rq=1>
- <https://www.reddit.com/r/TOR/comments/mou6ks/question_re_tortorifytorsocks_and_windows_os/>
- How To Install Netcat on Windows <https://www.configserverfirewall.com/windows-10/netcat-windows/>
- `socat`
  - <https://github.com/3ndG4me/socat/releases>
- `netcat`
  - <https://nmap.org/ncat/>
  - <https://nmap.org/dist/>
- `resistal`
  - <https://github.com/ResistalProxy/resistal/>

## Tor Setup on Linux Server

### Installation

> tbd.

### Get your onion address

> tbd.

```sh
# within the container
sudo cat /var/lib/tor/ssh/hostname
# from the host
sudo cat /data/ssh/hostname
```

---

## SSH Setup on Client Side

### Checking Tor Connection

- _Pifall 1_: Tor Browser on Windows has different port for **socks5** proxy:
  - Port `9150` for the Tor Browser.
  - If you install the Tor deamon on Windows, it should be port `9050` if the default settings haven't been altered.
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

### torify

```sh
torify ssh username@myonionaddress.onion
```

### netcat

```sh
ssh -o ProxyCommand='ncat --proxy-type socks5 --proxy 127.0.0.1:9050 %h %p' username@myonionaddress.onion
```

## Windows SSH Client over Tor Setup

### Putty

- Putty Configuration > Connection > Proxy:
  - Proxy type: `SOCKS 5`
  - Proxy hsotname: `127.0.0.1`
  - Port: `9150`
- Putty Configuration > Connection > SSH > Tunnels:
  - Forwarded ports: `L22 127.0.0.1`

### OpenSSH

```sh
ssh -o "ProxyCommand=ncat -x proxyhost:proxyport %h %p" -p port username@host
ssh -o "ProxyCommand=ncat -x 127.0.0.1:9150 %h %p" -p 22 username@myonionaddress.onion
ssh -o "ProxyCommand=ncat --proxy 127.0.0.1:9150 --proxy-type socks5 %h %p" -p 22 username@myonionaddress.onion
```

> Untested, unclear if this works in the `.ssh/config` file below:

```conf
Host myhost
  HostName myonionaddress.onion
     ProxyCommand ncat --proxy localhost:9150 --proxy-type socks5 %h %p
     User username
     Port 22
```

### cmder

## Tor Client Setup in Docker

- Setup Tor in a Docker Container
  - <https://sachsenhofer.io/setup-tor-docker-container/>
