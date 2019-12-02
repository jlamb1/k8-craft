start: set-env images k8-apply

images:
	docker build -f nginx/Dockerfile -t jlamb-nginx-php-fpm .

k8-apply:
	kubectl apply -k ./

set-env:
	eval $(minikube docker-env)

nginx:
	docker build -f nginx/Dockerfile -t jlamb-nginx .

php:
	docker build -f php/Dockerfile -t jlamb-php .