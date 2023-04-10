# Server Setup Process

# Docker (latest)

~~~
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update
apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
~~~

# Caddy

~~~
apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | tee /etc/apt/sources.list.d/caddy-stable.list
apt update
apt install caddy
~~~

# HTML / Config

~~~
mkdir -p /var/www/html

## Edit/replace /var/www/html/index.html
## see HTML file in repo

## Edit/replace /etc/caddy/Caddyfile
## see config file in repo
~~~

# AI tools
## [Dalai - Alpaca, llama](https://github.com/cocktailpeanut/dalai)

~~~
mkdir src
cd src
git clone https://github.com/cocktailpeanut/dalai.git
cd dalai
docker compose build
docker compose run dalai npx dalai alpaca install 7B
docker compose run dalai npx dalai llama install 7B 13B
~~~

## Stable Diffusion - [Docker web UI](https://github.com/AbdBarho/stable-diffusion-webui-docker/wiki/Setup)

~~~
git clone https://github.com/AbdBarho/stable-diffusion-webui-docker.git
cd stable-diffusion-webui-docker/
docker compose --profile download up --build
## UI that will use CPU
docker compose --profile auto-cpu up --build
~~~

## Whisper - [Docker Whisper web UI](https://codeberg.org/pluja/web-whisper/)

~~~
git clone https://codeberg.org/pluja/web-whisper
cd web-whisper
cp example.docker-compose.yml docker-compose.yml
vi docker-compose.yml
## change exposed port to 4000
cp example.env .env
docker compose up --build
~~~
