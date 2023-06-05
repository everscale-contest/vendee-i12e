# Team server infrastructure

![cover](docs/cover.svg)

![build](https://img.shields.io/github/actions/workflow/status/kokkekpek/vendee-i12e/deploy.yaml)

## Server [ansible](https://www.ansible.com) initialization

```shell
ansible-playbook -i playbook/inventory/all.yaml playbook/init.yaml
```

## Up local

```shell
docker network create traefik
docker compose --env-file .env.local up
```

## Deploy on server

### Set secrets

* `SSH_DEPLOY_PRIVATE_KEY` - e.g. `AAAwEAA ...`
* `BASIC_AUTH_USER` - e.g. `admin`
* `BASIC_AUTH_PASSWORD` - e.g. `admin`

### Run GitHub action manually

[Deploy action](https://github.com/kokkekpek/vendee-i12e/actions/workflows/deploy.yaml)

## Docker network scheme

```mermaid
flowchart TD
    %% Traefik
    traefik(traefik)-->|traefik|tempo(tempo)
    
subgraph Grafana
    tempo(tempo)
end
```