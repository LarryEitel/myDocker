# Build custom image

## From images folder

```
docker login -u larryeitel -p
docker build -t larryeitel/standalone-firefox-debug:0.1 images/selenium-custom
docker build -t larryeitel/standalone-firefox-debug:latest images/selenium-custom
```


## Push to docker hub

```
docker push larryeitel/standalone-firefox-debug:0.1
docker push larryeitel/standalone-firefox-debug:latest
```
