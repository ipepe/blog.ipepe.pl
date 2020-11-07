# How I created review apps on self hosted Gitlab


```yaml
# docker-compose.ra.yml
version: '3'
services:
  app:
    build:
      context: .
      dockerfile: reviewapp.Dockerfile
    restart: always
    network_mode: bridge
    healthcheck:
      disable: true
    expose:
      - 80
      - 443
    labels:
      - "traefik.enable=true"
      - "traefik.port=80"
      - "traefik.frontend.rule=Host:${CI_COMMIT_REF_NAME}.ra.skriware.host"
    container_name: 'skrimarket_${CI_COMMIT_REF_NAME}'

# docker-compose -f docker-compose.ra.yml up
```

