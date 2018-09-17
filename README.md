# Requirement
* docker
* docker-compose

# Install
```
docker-compose build
docker-compose start -d
docker-compose exec -w /opt/htdocs/unknown-ci/src php composer install
docker-compose exec mysql mysql -uroot -p{password} -e"create database ci;"
cp /opt/htdocs/unknown-ci/src/.env.example /opt/htdocs/unknown-ci/src/.env
chmod 777 -R /opt/htdocs/unknown-ci/src/storage
chmod 777 -R /opt/htdocs/unknown-ci/src/bootstrap/cache
docker-compose exec -w /opt/htdocs/unknown-ci/src php php artisan key:generate
docker-compose exec -w /opt/htdocs/unknown-ci/src php php artisan migrate
```
modify environment file `/opt/htdocs/unknown-ci/src/.env`