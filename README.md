#Steps to deploy redis using StatefulSet on Minikube


###Install Docker
https://docs.docker.com/engine/install/

###Install Minikube
https://minikube.sigs.k8s.io/docs/start/

Run below commands to start MiniKube
```
minikube start
```

For additional insight into your cluster state, minikube bundles the Kubernetes Dashboard, allowing you to get easily acclimated to your new environment:

```
minikube dashboard
```

###Install Helm
https://helm.sh/docs/intro/install/

###Install Helm chart for redis
```
helm install redis -f ci/standalone-values.yaml ./redis
```

after helm install use below steps to connect to redis

```
To get your password run:

    export REDIS_PASSWORD=$(kubectl get secret --namespace default redis -o jsonpath="{.data.redis-password}" | base64 --decode)

To connect to your Redis&trade; server:

1. Run a Redis&trade; pod that you can use as a client:

   kubectl run --namespace default redis-client --restart='Never'  --env REDIS_PASSWORD=$REDIS_PASSWORD  --image docker.io/bitnami/redis:6.2.5-debian-10-r63 --command -- sleep infinity

   Use the following command to attach to the pod:

   kubectl exec --tty -i redis-client \
   --namespace default -- bash

2. Connect using the Redis&trade; CLI:
   redis-cli -h redis-master -a $REDIS_PASSWORD

```