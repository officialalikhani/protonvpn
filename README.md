# Protonvpn Docker image

You can pull this image from my docker repository , See my repo "https://hub.docker.com/u/officialalikhani"


```bash
docker run \
--rm \
--detach \
--name=protonvpn \
--device=/dev/net/tun \
--cap-add=NET_ADMIN \
--env PROTONVPN_USERNAME="OpenVPN Username. This is NOT your Proton Account Username." \
--env PROTONVPN_PASSWORD="OpenVPN Password. This is NOT your Proton Account Password." \
--env PROTONVPN_TIER="Proton VPN Tier (0=Free, 1=Basic, 2=Pro, 3=Visionary) " \
--env PROTONVPN_SERVER="ProtonVPN server to connect to. See PROTONVPN_SERVER for more info" \
--env PROTONVPN_PROTOCOL="Protocol to use. By default udp is used." \
officialalikhani/protonvpn:protonvpn
```


If set to RANDOM, a random server compatible with your plan will be chosen.\
If set to P2P will choose fastest P2P server. Please note that this requires setting correct plan in PROTONVPN_TIER.\
If set to ProtonVPN supported country code, will choose the fastest server from this country. (case insensitive). For example to connect to fastest server from Netherlands, set PROTONVPN_SERVER to NL. \
If none of the above are true, container will attempt to connect to this server and fail if it is not possible. Please note that Secure Core servers are only available with pro plan and above. \


## Docker-compose
Lets see  the Docker-compose file 
```yml
version: '3.9'
services:
  protonvpn:
    container_name: "container_name"
    environment:
      PROTONVPN_USERNAME: "OpenVPN Username"
      PROTONVPN_PASSWORD: "OpenVPN Password"
      PROTONVPN_SERVER: "ProtonVPN server to connect"
      PROTONVPN_TIER: "Proton VPN Tier "
    image: "officialalikhani/protonvpn:protonvpn"
    restart: unless-stopped
    networks:
      - internet
      - proxy
    cap_add:
      - NET_ADMIN
    devices:
      - /dev/net/tun:/dev/net/tun
    expose:
      - 8000
volumes:
  config:
networks:
  internet:
  proxy:
    internal: true
```

