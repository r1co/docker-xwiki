# docker-xwiki

Forked from [hellyna](https://github.com/Hellyna/docker-xwiki). Updated to version 9.11.4. 

A basic working image for xwiki. 

# Usage

## Create persistence

Persistent volumes are already defined by the image, so there is no
need to explicitly define volumes using `-v`.

```shell
docker create \
  --name 'xwiki-persistence' \
  --entrypoint /bin/true \
  hellyna/xwiki:7.1
```

## Run!

Run with the above persistent container.

```shell
docker run -it --rm \
  --name 'xwiki' \
  --volumes-from 'xwiki-persistence' \
  -p 8080:8080 \
  r1co/docker-xwiki:latest
```

Try to point your browser to 'http://localhost:8080/' if you are running
a local instance of docker!

## Compose 

```yaml
version: '3.4'

services:
  xwiki:
    image: r1co/docker-xwiki
    ports:
      - 8080:8080
    volumes:
      - xwiki-data:/usr/local/tomcat/webapps/ROOT/WEB-INF
      - xwiki-data:/var/local/xwiki

volumes:
  xwiki-data:
  ```