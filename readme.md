# Setup

* Copy websockets-server folder to xxx, in the dir run command `docker build -t websocketsserver .`
* Copy eoian folder to xxx, in the dir run command `docker build -t eo .`
* Pull minio from Docker Hub `docker pull minio/minio`
* Create a volume to persistent data mapping `docker volume create el-vol`
* Run `docker compose up -d --restart unless-stopped` in this directory
* Create a bucket `compass-eo` in minio if it does not already exist

