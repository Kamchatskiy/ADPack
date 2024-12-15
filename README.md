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
    cd /home && git clone --single-branch https://github.com/kamchatskiy/ADPack adpack
    ```

1. Update `.env` file
2. Configure docker compose files.
*You need to open game services' ports in [Safeline's docker-compose file](./safeline/docker-compose.yml)*
Example:

    ```yaml
    name: safeline

    services:
      mgt:
        # !!!
        ports:
          - 20002:1443
          - 3000:3000 # if game services listen 3000 port

    ```

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

2. Patch game services so they are in `safeline-ce` network and don't have any published ports

    ```yaml
    services:
      service:
        ...
        networks:
            safeline-ce:
        ports: # remove this
            - 3000:3000 # remove this
        ...
    networks:
      safeline-ce:
        external: true
    ```

3. Check [official guide for configuration](https://docs.waf.chaitin.com/en/tutorials/Configuration) for the next steps

## Port mapping

| Service            | Port    |
|--------------------|---------|
| Portainer          | `20000` |
| Portainer Agent    | `20001` |
| SafeLine           | `20002` |
| Culhwch            | `20003` |
| Packmate           | `65000` |
