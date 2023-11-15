# Matrix server, Element Chat Client, and Keycloak SSO setup using Ansible and Docker

## Purpose

This repository contains Ansible playbooks for automating the deployment of Matrix (Synapse) server, Element (Matrix Web Client), and Keycloak SSO (Single Sign-On) in a Dockerized environment.

That is, it lets you join the Matrix network using your own `@<username>:<your-domain>` identifier, all hosted on your own server.

We run all services in Docker containers, which lets us have a predictable and up-to-date setup, across multiple supported distros and architectures (x86/amd64 being recommended).

[Installation](docs/README.md) (upgrades) and some maintenance tasks are automated using [Ansible](https://www.ansible.com/)


## Supported services

Using this playbook, you can get the following list of services configured on your server. Basically, this playbook aims to get you up-and-running with all the necessities around Matrix, without you having to do anything else.

**Note**: the list below includes optional or even some advanced components that you will most likely not need.
Sticking with the defaults is the best choice, especially for a new installation.
You can always re-run the playbook later to add or remove components.


### Homeserver

The `homeserver` is the backbone of the matrix system: in our deployment we use Synapse. [Synapse](https://github.com/matrix-org/synapse), synapse stores your data and manages your presence in the Matrix network [Link](docs/configuring-playbook-synapse.md) 

### Clients

We have multiple Web clients for Matrix that you can host on your own domains. in our deployment we use `Element`:[Element](https://app.element.io/), Element is a Web UI, which is configured to connect to your own Synapse server by default [Link](docs/configuring-playbook-client-element.md) 


### Server Components

Services that run on the server to make the various parts of your installation work.

| Name | Default? | Description | Documentation |
| ---- | -------- | ----------- | ------------- |
| [PostgreSQL](https://www.postgresql.org/)| ✓ | Database for Synapse. [Using an external PostgreSQL server](docs/configuring-playbook-external-postgres.md) is also possible. | [Link](docs/configuring-playbook-external-postgres.md) |
| [Coturn](https://github.com/coturn/coturn) | ✓ | STUN/TURN server for WebRTC audio/video calls | [Link](docs/configuring-playbook-turn.md) |
| [nginx](http://nginx.org/) | ✓ | Web server, listening on ports 80 and 443 - standing in front of all the other services. Using our own webserver [is possible](docs/configuring-playbook-own-webserver.md) | [Link](docs/configuring-playbook-nginx.md) |
| [Let's Encrypt](https://letsencrypt.org/) | ✓ | Free  SSL certificate, which secures the connection to the Synapse server and the Element web UI | [Link](docs/configuring-playbook-ssl-certificates.md) |

## Infrastructure Overview

Our Matrix/Keycloak installation utilizes the following components:

- **Denbi OpenStack:** An open-source cloud computing platform, providing scalable and flexible virtualized resources.
- **Ceph Storage:** A distributed object storage and file system designed to provide excellent performance, reliability, and scalability.


## Installation

To configure and install Matrix on the server, follow the [README in the docs/ directory](docs/README.md).

## Features

- **Matrix Server (Synapse):** Decentralized communication platform.
- **Element Chat Client:** User-friendly interface for Matrix.
- **Keycloak SSO:** Centralized authentication and authorization.
- **Ansible Playbooks:** Automated deployment and configuration.
- **Docker:** Containerization for seamless deployment.
- **de.NBI Cloud:** Scalable cloud infrastructure.
- **Ceph Storage:** Distributed and scalable storage solution.

## Prerequisites

Before running the Ansible playbooks, ensure the following prerequisites are met:

- Ansible installed on the control machine where you plan to run the playbook.
- Docker installed on target servers.
- Target servers reachable from the control machine.
- SSH access configured for target servers.
- Cloud account and access credentials.
- Ceph storage configured in the cloud environment.

## Configuration
- Inventory File: Modify the inventory file with the target server details.
- In the `roles` repository, there are sub-repositories for Matrix, Keycloak, and nginix-proxy. Edit Variables, yml files, and config files located in each sub-repository to match your environment.
  
## Access URLs

- Matrix Server (Synapse): http://matrix-server_ip
- Element Chat Client: http://your-element-client
- Keycloak SSO: http://keycloak_instance_ip



### Bridges

Bridges can be used to connect the matrix installation with third-party communication networks.

| Name | Default? | Description | Documentation |
| ---- | -------- | ----------- | ------------- |
[mautrix-discord](https://github.com/mautrix/discord) | x | Bridge for bridging Matrix server to [Discord](https://discord.com/) | [Link](docs/configuring-playbook-bridge-mautrix-discord.md) |
| [mautrix-telegram](https://github.com/mautrix/telegram) | x | Bridge for bridging Matrix server to [Telegram](https://telegram.org/) | [Link](docs/configuring-playbook-bridge-mautrix-telegram.md) |
| [mautrix-whatsapp](https://github.com/mautrix/whatsapp) | x | Bridge for bridging Matrix server to [WhatsApp](https://www.whatsapp.com/) | [Link](docs/configuring-playbook-bridge-mautrix-whatsapp.md) |
| [mautrix-facebook](https://github.com/mautrix/facebook) | x | Bridge for bridging Matrix server to [Facebook](https://facebook.com/) | [Link](docs/configuring-playbook-bridge-mautrix-facebook.md) |
| [mautrix-twitter](https://github.com/mautrix/twitter) | x | Bridge for bridging Matrix server to [Twitter](https://twitter.com/) | [Link](docs/configuring-playbook-bridge-mautrix-twitter.md) |
| [mautrix-hangouts](https://github.com/mautrix/hangouts) | x | Bridge for bridging Matrix server to [Google Hangouts](https://en.wikipedia.org/wiki/Google_Hangouts) | [Link](docs/configuring-playbook-bridge-mautrix-hangouts.md) |
| [mautrix-googlechat](https://github.com/mautrix/googlechat) | x | Bridge for bridging Matrix server to [Google Chat](https://en.wikipedia.org/wiki/Google_Chat) | [Link](docs/configuring-playbook-bridge-mautrix-googlechat.md) |
| [mautrix-instagram](https://github.com/mautrix/instagram) | x | Bridge for bridging Matrix server to [Instagram](https://instagram.com/) | [Link](docs/configuring-playbook-bridge-mautrix-instagram.md) |
| [mautrix-signal](https://github.com/mautrix/signal) | x | Bridge for bridging Matrix server to [Signal](https://www.signal.org/) | [Link](docs/configuring-playbook-bridge-mautrix-signal.md) |
| [beeper-linkedin](https://github.com/beeper/linkedin) | x | Bridge for bridging Matrix server to [LinkedIn](https://www.linkedin.com/) | [Link](docs/configuring-playbook-bridge-beeper-linkedin.md) |
| [matrix-appservice-irc](https://github.com/matrix-org/matrix-appservice-irc) | x | Bridge for bridging Matrix server to [IRC](https://wikipedia.org/wiki/Internet_Relay_Chat) | [Link](docs/configuring-playbook-bridge-appservice-irc.md) |
| [matrix-appservice-discord](https://github.com/Half-Shot/matrix-appservice-discord) | x | Bridge for bridging Matrix server to [Discord](https://discordapp.com/) | [Link](docs/configuring-playbook-bridge-appservice-discord.md) |
| [matrix-appservice-slack](https://github.com/matrix-org/matrix-appservice-slack) | x | Bridge for bridging Matrix server to [Slack](https://slack.com/) | [Link](docs/configuring-playbook-bridge-appservice-slack.md) |
| [matrix-appservice-webhooks](https://github.com/turt2live/matrix-appservice-webhooks) | x | Bridge for slack compatible webhooks ([ConcourseCI](https://concourse-ci.org/), [Slack](https://slack.com/) etc. pp.) | [Link](docs/configuring-playbook-bridge-appservice-webhooks.md) |
| [matrix-hookshot](https://github.com/Half-Shot/matrix-hookshot) | x | Bridge for bridging Matrix to generic webhooks and multiple project management services, such as GitHub, GitLab, Figma, and Jira in particular | [Link](docs/configuring-playbook-bridge-hookshot.md) |
| [matrix-sms-bridge](https://github.com/benkuly/matrix-sms-bridge) | x | Bridge for bridging Matrix server to SMS | [Link](docs/configuring-playbook-bridge-matrix-bridge-sms.md) |
| [Heisenbridge](https://github.com/hifi/heisenbridge) | x | Bridge for bridging Matrix server to IRC bouncer-style | [Link](docs/configuring-playbook-bridge-heisenbridge.md) |
| [go-skype-bridge](https://github.com/kelaresg/go-skype-bridge) | x | Bridge for bridging Matrix server to [Skype](https://www.skype.com) | [Link](docs/configuring-playbook-bridge-go-skype-bridge.md) |
| [mx-puppet-slack](https://hub.docker.com/r/sorunome/mx-puppet-slack) | x | Bridge for bridging Matrix server to [Slack](https://slack.com) | [Link](docs/configuring-playbook-bridge-mx-puppet-slack.md) |
| [mx-puppet-instagram](https://github.com/Sorunome/mx-puppet-instagram) | x | Bridge for Instagram-DMs ([Instagram](https://www.instagram.com/)) | [Link](docs/configuring-playbook-bridge-mx-puppet-instagram.md) |
| [mx-puppet-twitter](https://github.com/Sorunome/mx-puppet-twitter) | x | Bridge for Twitter-DMs ([Twitter](https://twitter.com/)) | [Link](docs/configuring-playbook-bridge-mx-puppet-twitter.md) |
| [mx-puppet-discord](https://github.com/matrix-discord/mx-puppet-discord) | x | Bridge for [Discord](https://discordapp.com/) | [Link](docs/configuring-playbook-bridge-mx-puppet-discord.md) |
| [mx-puppet-groupme](https://gitlab.com/xangelix-pub/matrix/mx-puppet-groupme) | x | Bridge for [GroupMe](https://groupme.com/) | [Link](docs/configuring-playbook-bridge-mx-puppet-groupme.md) |
| [mx-puppet-steam](https://github.com/icewind1991/mx-puppet-steam) | x | Bridge for [Steam](https://steamapp.com/) | [Link](docs/configuring-playbook-bridge-mx-puppet-steam.md) |
| [Email2Matrix](https://github.com/devture/email2matrix) | x | Bridge for relaying email messages to Matrix rooms | [Link](docs/configuring-playbook-email2matrix.md) |


## Changes

This playbook evolves over time, sometimes with backward-incompatible changes.

When updating the playbook, refer to [the changelog](CHANGELOG.md) to catch up with what's new.


## Acknowledgments
This project is based on the work of [matrix ansible](https://github.com/spantaleev/matrix-docker-ansible-deploy).
