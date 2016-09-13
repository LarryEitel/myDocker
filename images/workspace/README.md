# Build custom image

## From images folder

```
docker login -u larryeitel -p
docker build -t larryeitel/dk_workspace:0.1 images/workspace
docker build -t larryeitel/dk_workspace:latest images/workspace
```


## Push to docker hub

```
docker push larryeitel/dk_workspace:0.1
docker push larryeitel/dk_workspace:latest
```
