# docker-registry
Docker Registry

## Quick Start

- Create `./config/auth` directory.
- Create the basic authentication: `docker run --entrypoint htpasswd httpd:2 -Bbn testuser testpassword > ./config/auth/htpasswd`.
- Create the certificate: `openssl req -newkey rsa:4096 -nodes -sha256 -keyout ./config/certs/domain.key -x509 -days 365 -out ./config/certs/domain.crt`.
- Start docker container: `docker compose up` or `docker compose up -d`.
- Deploy a [registry server](https://docs.docker.com/registry/deploying/).
- Config [insecure registry](https://docs.docker.com/registry/insecure/).
- Registry API example `curl -u '<docker_user>:<docker_password>' -v -X GET https://<registry_address>/v2/<repos_name>/tags/list`. Refer to [Registry API](https://docs.docker.com/registry/spec/api/#detail).
- Refer to docker compose document in [here](https://docs.docker.com/compose/overview/#compose-documentation).

## Garbage Collection

- Clear disk space by [garbage collection](https://docs.docker.com/registry/garbage-collection/). Ex: `docker exec registry bin/registry garbage-collect /etc/docker/registry/config.yml -m`.
- Clear disk space automatically by command: `crontab -e`, add more content as (every hour):
```
0 * * * * docker image prune -f
0 * * * * docker volume prune -f
0 * * * * docker exec registry bin/registry garbage-collect /etc/docker/registry/config.yml -m
```
