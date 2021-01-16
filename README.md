# TURN server via docker for Nextcloud Talk

For this project to work, you will have to also install the `traefik-docker` project available [here](https://github.com/m1rkwood/traefik-docker).

## Setup your DNS

Setup your subdomain so that when you're ready, it's already pointing to the right direction. Simply go to your DNS provider, and create a `A` record with the information needed:

```
Type: A Record
Host:
Value: IP-OF-YOUR-SERVER
TTL:
```

For `Host`, choose whatever subdomain you want to host at.
For `TTL`, I used the lowest available or `Automatic`

## Envionment

Duplicate the `.env.template` and rename it to `.env`  
In the `.env` file, add the information necessary  

This is the information about your domain, for example if you want to host the server at `stuff.example.com`:
```
SUBDOMAIN=stuff
DOMAIN=example.com
```
This is the IP of your server:
```
EXTERNAL_IP=
```
Generate a strong password and place it here:
```
STATIC_AUTH_SECRET=
```
For port configuration, you can refer to this [documentation](https://github.com/instrumentisto/coturn-docker-image):
```
LISTENING_PORT=
MIN_PORT=
MAX_PORT=
```

## Run the container

```
docker-compose up -d
```

## Configuration with Nextcloud Talk

Make sure you have the App `Nextcloud Talk` installed on your Nextcloud instance.

Full documentation available [here](https://nextcloud-talk.readthedocs.io/en/latest/TURN/)  

> Go to Nextcloud admin panel > Talk settings. Btw. if you already have your own TURN server, you can and may want to use it as STUN server as well:  
> STUN servers: your.domain.org:  
> TURN server: your.domain.org:  
> TURN secret:  
> Protocol: UDP and TCP  
> Do not add http(s):// or turn(s):// protocol prefix here, just enter the bare domain:port. Nextcloud Talk adds the required turn:// protocol internally to the request.  

