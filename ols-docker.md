## Clone repo from git: 

```
git clone https://github.com/litespeedtech/ols-docker-env.git
```
## Before run or start the installtion, Take a a look .env file. make required changed and then go on

## run docker project

```
docker compose up -d
```
## Before run database command add domain first to initialize domain. Then run 
```
bash bin/domain.sh --add example.com
bash bin/database.sh --domain example.com
```
## useful commands
```
docker compose stop
docker compose down

bash bin/webadmin.sh my_password
bash bin/demosite.sh

bash bin/domain.sh --add example.com
bash bin/domain.sh --del example.com
bash bin/database.sh --domain example.com
bash bin/database.sh --domain example.com --user USER_NAME --password MY_PASS--database DATABASE_NAME
./bin/appinstall.sh --app wordpress --domain example.com
./bin/acme.sh --install --email EMAIL_ADDR
./bin/acme.sh --install --no-email
./bin/acme.sh --domain example.com
bash bin/webadmin.sh --upgrade
bash bin/webadmin.sh --mod-secure enable
bash bin/webadmin.sh --mod-secure disable
```



## Customization
If you want to customize the image by adding some packages, e.g. lsphp74-pspell, just extend it with a Dockerfile.

We can create a custom folder and a ```custom/Dockerfile``` file under the main project.
Add the following example code to Dockerfile under the custom folder
```
FROM litespeedtech/openlitespeed:latest
RUN apt-get update && apt-get install lsphp74-pspell -y
```
Add build: ./custom line under the "image: litespeedtech" of docker-composefile. So it will looks like this
```
  litespeed:
    image: litespeedtech/openlitespeed:${OLS_VERSION}-${PHP_VERSION}
    build: ./custom
```
Build and start it with command:
```
docker compose up --build
```
