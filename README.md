# k8s-workshop

## Create local kind cluster
kind create cluster --config cluster.yaml
kind get clusters
kind get nodes
docker ps

## Configure CLI access
kubectl cluster-info --context kind-kind
cat $HOME/.kube/config
kubectl version --short
kubectl get nodes
kubectl get --all-namespaces pods

## Install User Interface
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl apply -f ui-service-account.yaml

kubectl proxy (in a different terminal)
Go to  http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login

kubectl -n kubernetes-dashboard create token admin-user

## Imperative commands
kubectl run nginx --image=nginx
kubectl run another-nginx --image=nginx

## Declarative commands
kubectl create namespace example
kubectl apply -f pod.yaml

## Deployments
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/examples/2048/2048_full.yaml
Go to http://localhost:8001/api/v1/namespaces/game-2048/services/http:service-2048:/proxy/

kubectl apply -f deployment.yaml
Go to http://localhost:8001/api/v1/namespaces/example/services/http:example-service:/proxy/

## Cleanup
kind delete cluster

## Custom images
./kind-with-registry.sh

docker build -t localhost:5001/example .
kubectl create namespace example
kubectl apply -f local-deployment.yaml

Go to http://localhost:8001/api/v1/namespaces/example/services/http:example-local-service:/proxy/
