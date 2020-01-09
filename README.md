# Craft on Kubernetes

This is intended as a boilerplate to get started using Craft locally. It is not production ready!

## System Requirements

One of the two:
- [Docker for Desktop](https://www.docker.com/products/docker-desktop)
    - enable Kubernetes in preferences after install
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)

Optional:
- [VirtualBox](https://www.virtualbox.org/) - if you'd prefer not to use hyperkit, or not on mac
- [Garden.io](https://garden.io/)

Garden is optional as you can deploy regularly with kubernetes/kubectl directly. However, it's highly recommended as it makes deployment much simpler and adds hot reloading.

## Quick Start

- clone repo
    - add `.env` file inside /app
- from root of repo, run these scripts
    - if running minikube: `minikube start` `eval $(minikube docker-env)`
    - `docker build -f nginx/Dockerfile -t jlamb-nginx .`
    - `docker build -f php/Dockerfile -t jlamb-php .`
    - one of the two:
        - `kubectl apply -k ./` - if using kubectl directly
        - `garden dev` - if using Garden
    - `minikube dashboard` - optional, to see deploy status. you will need to leave this terminal window open

Once the deployment is live:
- enter the php pod via `kubectl exec -it php /bin/bash` (add `-n craftcms` if using Garden)
- run `./craft install` to setup your first user.
- Finally, run `rm -rf storage/*` to clear a permissions problem. exit the container.

run `minikube service craft --url` to get the link for your site, it should open to the welcome screen. If using Garden, the link is available directly in the terminal.

### Troubleshooting

If using Dnsmasq (Valet), you may need to run `sudo brew services stop dnsmasq` to allow minikube to resolve correctly