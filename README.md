### Decrypt
You need key
```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -in \
    ./dummy-image.tar.gz.enc -out ./dummy-image.tar.gz -pass file:./mykey.key

openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -in \
    ./dummy-image-helper.tar.gz.enc -out ./dummy-image-helper.tar.gz -pass file:./mykey.key
```
### Load
```bash
docker load < dummy-image-helper.tar.gz
docker load < dummy-image.tar.gz
```
### Run
```bash
docker run  --network=host -e DISPLAY=$DISPLAY  -v /tmp/.X11-unix:/tmp/.X11-unix --rm dummy-image:latest
docker run  --network=host -e DISPLAY=$DISPLAY  -v /tmp/.X11-unix:/tmp/.X11-unix --rm dummy-image-helper:latest
```