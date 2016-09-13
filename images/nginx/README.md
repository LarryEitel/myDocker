# Build custom image

## From images folder

```
docker login -u larryeitel -p
docker build -t larryeitel/dk_nginx:0.1 images/nginx
docker build -t larryeitel/dk_nginx:latest images/nginx
```


## Push to docker hub

```
docker push larryeitel/dk_nginx:0.1
docker push larryeitel/dk_nginx:latest
```
