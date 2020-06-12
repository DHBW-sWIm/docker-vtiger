# swimdhbw/vtiger

Vtiger CRM is open source software that helps more than 100000 businesses grow sales,
improve marketing reach, and deliver great customer service.

This repository contains a modified version of VTiger 7.1.0 according to SWIM CRM requirements.
You can upgrade to a newer version of VTiger by modifying the Dockerfile. Please referr to [this repository](https://github.com/javanile/vtiger). There you can find further information about other Dockerfile configurations.

## Docker Hub

Based on this repository Docker Hub will generate a docker image by using an automatic build pipeline. It is available under: [swimdhbw/vtiger](https://hub.docker.com/r/swimdhbw/vtiger).
You can use it in order to deploy it locally or on our SWIM Kubernetes Cluster.

## Try with Docker Compose

Create your custom vtiger environment locally, follow this as example:

```yaml
version: '3'

services:
  vtiger:
    image: swimdhbw/vtiger:latest
    environment:
      - VT_SITE_URL=http://localhost:8080
      - MYSQL_HOST=mysql
      - MYSQL_DATABASE=vtiger
      - MYSQL_ROOT_PASSWORD=secret
    ports:
      - 8080:80
    volumes:
      - ./:/app
      - vtiger:/var/lib/vtiger
    links:
      - mysql

  mysql:
    image: mysql:5.5
    environment:
      - MYSQL_DATABASE=vtiger
      - MYSQL_ROOT_PASSWORD=secret
    volumes:
      - mysql:/var/lib/mysql:rw

volumes:
  mysql:
  vtiger:
```