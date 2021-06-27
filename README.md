# docker-registry
Docker Registry

## Quick Start

- Create `./data/auth` directory.
- Create the basic authentication: `docker run --entrypoint htpasswd registry:2.7.0 -Bbn testuser testpassword > ./data/auth/htpasswd`.
- Create the certificate: `openssl req -newkey rsa:4096 -nodes -sha256 -keyout ./data/certs/domain.key -x509 -days 365 -out ./data/certs/domain.crt`.
- Start docker container: `docker-compose up` or `docker-compose up -d`.
- Deploy a [registry server](https://docs.docker.com/registry/deploying/).
- Config [insecure registry](https://docs.docker.com/registry/insecure/).
- Clear disk space by [garbage collection](https://docs.docker.com/registry/garbage-collection/). Ex: `docker exec registry bin/registry garbage-collect /etc/docker/registry/config.yml -m`.
- Registry API example `curl -u '<docker_user>:<docker_password>' -v -X GET https://<registry_address>/v2/<repos_name>/tags/list`. Refer to [Registry API](https://docs.docker.com/registry/spec/api/#detail).
- Refer to docker compose document in [here](https://docs.docker.com/compose/overview/#compose-documentation).
