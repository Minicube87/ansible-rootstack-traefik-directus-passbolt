# Project

This is the project repository for the final project of the vocational training as an IT specialist for system integration by Jan Sulga, focusing on "Automated Setup of a Root Server Including Two Web Applications Using Ansible." This final project was completed in 2024.
Sensitive data has been redacted for the public repository.

This repository includes an Ansible folder with the corresponding Ansible playbooks, as well as project folders for each of the individual services.

## Architecture overview

- Provision and harden a Debian root server, create an admin user, and install Docker + Fail2Ban.
- Deploy Traefik as the edge reverse proxy with ACME TLS and middleware for auth/IP allow-listing.
- Run Directus (Postgres + Redis) and Passbolt (MariaDB) behind the proxy using Docker Compose.
- Use Ansible Vault for app-specific .env files; placeholders in this repo are safe for public sharing.

## Prerequisites

- Debian 11 (target host)
- Ansible on the control machine
- SSH access to the target host (key-based)
- Ansible Vault password for decrypting app .env files

## Secrets and configuration

- Real credentials live in Ansible Vault-managed `.env` files.
- Public repo contains placeholders; replace them before deploying.

## Stack

- Ansible (provisioning)
- Docker / Docker Compose (runtime)
- Traefik (reverse proxy + TLS)
- Directus + Postgres + Redis
- Passbolt + MariaDB

## Order of execution of the playbooks

1. Rootserver
    1. Prepare

        ``` shell
        ansible-playbook pb1_prepare.yml --ask-become-pass 
        ```

    2. Setup

        ```shell
        ansible-playbook pb2_setup.yml --ask-become-pass 
        ```

    3. Traefik

        ``` shell
        ansible-playbook pb3_traefik.yml --ask-become-pass 
        ```

2. Applications
   1. Directus

        ```shell
        ansible-playbook pb4_directus.yml 
        ```

   2. Passbolt

        ```shell
        ansible-playbook pb5_passbolt.yml
        ```
