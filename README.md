# Kubernetes Demo with yelb

This repo contains sample deployment files that will deploy the [yelb][yelb-gh] sample
app. Please see the linked repo for more details on what the application is.

## Installing

The manifests are broken down into 5 different parts for ease of use:

- `0-namespace.yaml`: deploys a namespace for the application
- `1-redis.yaml`: used for caching data
- `2-db.yaml`: the DB for the application
- `3-appserver.yaml`: deploys the actual application server
- `4-ui.yaml`: deploys the front end

For demo purposes, [minikube][minikube] was used to deploy these files and play around
with the application and its behaviour within Kubernetes.

To deploy to your cluster, run the following command:

- `kubectl apply -f <name_of_file>` going sequentially down the list
- `kubectl apply -f ./` to deploy the entire folder

## Using the Application

Check the status of your pods:

- `kubectl get pods -A` checks the pods in ALL namespaces
- `kubectl get pods -n yelb` to get the pods in just this namespace

To view your application:

- `kubectl port-forward service/yelb-ui 3001:80`: this creates a port forward on your
local machine to the UI service. Go to `http://localhost:3001` to see the application

Play with your pods:

- `kubectl scale deployment --replicas=3 -n yelb yelb-appserver` to scale the application
server to 3 pods. Refresh the page to see the various app servers serving traffic. You
can do the same for the other deployment objects
- `kubectl logs -n yelb <pod name>` to see stdout logs on your container

## Uninstalling

Delete your deployment by running `kubectl delete -f ./` to delete all the manifests

[yelb-gh]: https://github.com/mreferre/yelb
[minikube]: https://minikube.sigs.k8s.io/docs/start/