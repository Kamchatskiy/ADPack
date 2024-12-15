# ADPack

## Pack of tools for Attack-Defense CTF competitions

## Tools

- [Portainer](https://github.com/portainer/portainer): GUI service for managing docker containers
  - Standalone
  - Agent: in case you have an own local Portainer instance running
- [Safeline](https://github.com/chaitin/SafeLine): Web Application Firewall (WAF)
- [Packmate](https://gitlab.com/packmate/Packmate): Traffic sniffer
- [Culhwch](https://github.com/arkiix/CulhwchFarm): Exploit farm

## Setup

On a virtual machine

0. Clone repository

    ```shell
    cd /home && git clone https://github.com/kamchatskiy/ADPack adpack
    ```

1. Update `.env` file
2. Configure docker compose files.
*You need to open game services' ports in [Safeline's docker-compose file](./safeline/docker-compose.yml)*
3. Run with:

    ```shell
    docker compose --env-file .env --profile all up -d
    ```

### Profiles

You can choose what service to start using compose profiles

Specify them like
    ```
    docker compose --profile profile1 --profile profile2 ...
    ```

- `all` - run all tools available
- `portainer_agent`
- `portainer_app`
- `culhwch`
- `packmate`

## Post-Setup

### Safeline

1. Configure Safeline creds

    ```shell
    docker exec safeline-mgt resetadmin
    ```

2. Patch game services so they are in `safeline-ce` network

    ```yaml
    services:
      service:
        ...
        networks:
            safeline-ce:
        ...
    networks:
      safeline-ce:
        external: true
    ```

## Port mapping

| Service            | Port    |
|--------------------|---------|
| Portainer          | `20000` |
| Portainer Agent    | `20001` |
| SafeLine           | `20002` |
| Culhwch            | `20003` |
| Packmate           | `65000` |
