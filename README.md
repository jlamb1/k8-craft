# Craft on Kubernetes

This is intended as a boilerplate to get started using Craft locally. It is not production ready!

## System Requirements

This has been tested on mac, and may require tweaks

- [Docker for Desktop](https://www.docker.com/products/docker-desktop)
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)

## Quick Start

- clone repo
    - `cd app && composer install`
- from root of repo, run these scripts
    - `minikube start`
    - `eval $(minikube docker-env)`
    - `docker build -f nginx/Dockerfile -t jlamb-nginx .`
    - `docker build -f php/Dockerfile -t jlamb-php .`
    - `kubectl apply -k ./`
    - `minikube dashboard` - optional, to see deploy status. you will need to leave this terminal window open

Once the deployment is live:
- enter the php pod via `kubectl exec -it php /bin/bash`
- run `./craft install` to setup your first user.
- Finally, run `rm -rf storage/*` to clear a permissions problem. exit the container.

run `minikube service craft --url` to get the link for your site, it should open to the welcome screen
