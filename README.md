# Current Steps (yikes)

- git clone && cd in

- `minikube start`

- `eval $(minikube docker-env)`

- `docker build -f nginx/Dockerfile -t jlamb-nginx .`

-  `docker build -f php/Dockerfile -t jlamb-php .`

- `kubectl apply -k ./`

- `kubectl exec -it php /bin/bash`

- `./craft setup`

- `rm -rf storage/runtime`