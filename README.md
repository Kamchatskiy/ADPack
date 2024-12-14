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
*You need to open services' ports in [Safeline's docker-compose file](./safeline/docker-compose.yml)*
3. Run with:

    ```shell
    docker compose --env-file .env --profile all up -d
    ```

## Profiles

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

## Port mapping

| Service            | Port   |
|--------------------|--------|
| Portainer          | `9443` |
| Portainer Agent    | `9001` |
| Packmate           | `65000`|
| SafeLine           | `9444` |
