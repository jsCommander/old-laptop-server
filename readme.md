# Media Server from an Old Laptop

Got an old laptop lying around at home? Turn it into a trendy server! With some simple manipulations, your laptop can:

1. Download and distribute torrents
2. Stream movies to various devices

Used repositories:

1. [docker-transmission](https://github.com/linuxserver/docker-transmission)
2. [docker-plex](https://github.com/linuxserver/docker-plex)

## Installation

1. Install Docker

   ```bash
   sudo apt install docker.io
   ```

2. Add the current user to the docker group to use it without sudo

   ```bash
   sudo usermod -aG docker $USER
   ```

3. Fill `.env` file

   ```env
   ROOT_PATH=/home/user/
   TRANSMISSION_USER=someuser
   TRANSMISSION_PASS=somepass
   ```

4. Start containers

   ```bash
   docker compose up -d
   ```

5. Check services:
   - **transmission-web-client:** http://localhost:9091/
   - **plex-web:** http://localhost:32400/web

## Lid-switch

To prevent the laptop from turning off when the lid is closed, ignore the lid-switch.
Open /etc/systemd/logind.conf in any editor

```bash
sudo vim /etc/systemd/logind.conf
```

and create/edit the line there (the line should not have a comment symbol #)

` HandleLidSwitch=ignore

Restart the service

```bash
sudo systemctl restart systemd-logind
```
