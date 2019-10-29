# RTMP RELAY SEVER
Kubernetes deployment of an RTMP server that relays an input livestream to multiple channels.
The solution is based on the public docker image: `alfg/docker-nginx-rtmp`.

## Build Docker Image

Build a local docker image. The image is tagged here as `esw-rtmp-server`.
```
> docker build -t esw-rtmp-server .
```

## Push Image to Repository
- Make sure to have an account in a docker registry, for instance Docker Hub.
- Create a repository in your hosting service (here it is named `sb/esw-rtmp-server`)
- Login to your docker account in your local environment and then push the previously built docker image to your hosted repository. 

```
> docker tag esw-rtmp-server sb/esw-rtmp-server 
> docker push sb/esw-rtmp-server 
```

## Deploy to k8s
- Make sure to have an operational  kubernetes cluster (Local or hosted by your service provider)

- Apply the project deployment to create a pod running the server in your cluster.
```
> kubectl apply -f k8s/Deployment.yml
```

- Expose the pod via a load balancer in order to receive incoming HTTP traffic.
```
> kubectl apply -f k8s/Service.yml
```

## RTMP Stream information

Check the external IP address of the deployed service. 
```
> kubectl get service esw-rtmp
```

The RTMP stream that the server will relay is:

### rtmp://`[EXTERNAL-IP]`:1935/stream/ 
