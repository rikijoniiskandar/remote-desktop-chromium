# How to Get Timezone?
run `realpath --relative-to /usr/share/zoneinfo /etc/localtime`

# How to run?
1. run `mkdir chromevps && cd chromevps && nano compose.yaml`
2. paste the content of `compose.yaml` file
```
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=root #Change with your desire username
      - PASSWORD=myPassword #Change with your desire password
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Jakarta # must match your VPS timezone run "realpath --relative-to /usr/share/zoneinfo /etc/localtime" to get the timezone name
      - CHROME_CLI=https://github.com/yornfifty #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped
```
3. save and run `docker compose up -d`
3. open `YOUR_VPS_IP:3010` anywhere on your pc's browser
