# Local Dev Setup

* Copy websockets-server folder to xxx, in the dir run command `docker build -t websocketsserver .`
* Copy eoian folder to xxx, in the dir run command `docker build -t eo .`
* Pull minio from Docker Hub `docker pull minio/minio`
* Create a volume to persistent data mapping `docker volume create el-vol`
* Run `docker compose up -d --restart unless-stopped` in this directory
* Create a bucket `compass-eo` in minio if it does not already exist


# Deploy to server
A .env file is used to set the WEBAPIKEY environment variable and have it persist across restarts and re-deployments/updates
The .env file is created on first deployment only, and is not overwritten on subsequent deployments unless needed
The API key is just a long password and is stored in LastPass under name eo-stack config

Commands:

    #local:
    git archive main --output deploy.zip 
    pscp deploy.zip eouser@eo-stack:/home/eouser/

    #remote:
    unzip deploy.zip -d compose-tmp
    rm ./compose-tmp/.env
    cp -a ./compose-tmp/. compose/
    rm -r compose-tmp
    cd compose

    # Only need to run this on first deploy or if changing API key
    echo "WEBAPIKEY = xxx" > .env

    docker-compose down
    docker-compose up -d
