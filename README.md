## Plex + Transmission

This project aims to create a bundled project to pull up Plex server and Transmission-cli together and make them work together seamlessly.

The project can be coupled with this [Loadbalancer](https://github.com/jwilder/docker-gen) based on nginx-proxy, dockergen and letsencrypt to automatically handle routing and https.

## Requirements

You don't need [Loadbalancer](https://github.com/jwilder/docker-gen) if you already have a similar solution set up as long as they make use of the environment variables `VIRTUAL_HOST` and `LETSENCRYPT_HOST`

You'll need **Docker** and **Docker Compose** to test this out.

## Configuration

### Plex

To configure Plex, you'll need to edit the file *Preferences.sample.xml*. You'll find the file in `./config/plex/Library/Application Support/Plex Media Server/`
- Rename it to **Preferences.xml**
- Update `customConnections` to your **ADVERTISE_IP** (See below)
- Set `PlexOnlineToken`, you can get this on plex.com
- Set `PlexOnlineUsername` with your plex.com username
- Update `PlexOnlineMail` with the email you use on plex.com
- Finally set a friendly name for your server by setting `FriendlyName`

### Transmission

For Transmission, edit *settings.samle.json* which you'll find in `./config/ts/`

- Rename the file to `settings.json`
- Set `rpc-host-whitelist` to your domain for this container (See below **VIRTUAL_HOST_TS**)
- Set your password by updating `rpc-password`. After you login the first time, Transmission will hash it automatically
- And finally set a username `rpc-username`

### General config

Now some configuration to expose the containers and make them accessible

- Rename `.env.sample` to `.env` in the project root folder
- Set `VIRTUAL_HOST_PLEX` to the domain you want to use to access **Plex Server** and `VIRTUAL_HOST_TS` for the domain you want for Transmission
- To add **https** you must set `LETSENCRYPT_EMAIL_PLEX` for Plex and `LETSENCRYPT_EMAIL_TS` for Transmission
- You need to set `PLEX_CLAIM` to bind your server to your plex.com account
- Also set `PLEX_HOSTNAME` to the domain you want Plex to have. It should be the same as one of the values in **VIRTUAL_HOST_PLEX**
- To wrap it up, set `PLEX_ADVERTISE_IP` to the ip reaching your server or a dedicated domain.

## Notice

This is just a proof of concept. I cannot be liable if you use this project for piracy or otherwise illegal activity.