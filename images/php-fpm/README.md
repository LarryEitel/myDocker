# Build custom image

## From images folder

```
docker login -u larryeitel -p
docker build -t larryeitel/dk_php-fpm:0.1 images/php-fpm
docker build -t larryeitel/dk_php-fpm:latest images/php-fpm
```


## Push to docker hub

```
docker push larryeitel/dk_php-fpm:0.1
docker push larryeitel/dk_php-fpm:latest
```
