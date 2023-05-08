# k8s-beginner-lvl
This is a playground repo for absolute k8s beginners

Kubernetes Deployment and Service Creation

## Prerequisites

Before you start, you should have the following:

- Kubernetes cluster
- `kubectl` command line tool installed and configured to communicate with your Kubernetes cluster
- Docker installed on your local machine

## Make Custom Docker Image

- Create a docker hub account if you don't have
  

1. Create a Dockerfile in the directory of your Node.js web app:
  

```
FROM node:alpine

WORKDIR /app

EXPOSE 3000

COPY package.json package-lock.json ./

RUN npm install

COPY . ./

CMD ["npm", "start"]
```

2. Build the docker image using `docker build` command:
  

```
docker build -t tay98/k8s-web-hello:v1 .
```

3. Test the docker image locally using `docker run` command:
  

```
docker run -p 3000:3000 tay98/k8s-web-hello:v1
```

4. Verify that your Node.js web app is running by navigating to
  

`http://localhost:3000` in a web browser

5. Push the docker image to Docker Hub using the `docker push` command:
  

```
docker push tay98/k8s-web-hello:v1
```

This will push the Docker image to Docker Hub, and make it available to deploy in kubernetes.

## Deployment

1. Create a kubernetes deployment using the `kubectl create deployment` command:
  
  ```
  kubectl create deployment my-app --image=tay98/k8s-web-hello
  ```
  
2. Check the status of the deployment using the `kubectl get deployments` command:
  

```
kubectl get deployments
```

3. Scale up the deployment using the `kubectl scale` command:
  

```
kubectl scale deployment my-app --replicas=5
```

## Service

1. Create a kubernetes service using the `kubectl expose` command:
  

```
kubectl expose deployment my-app --port=3030 --target-port=3000 --type=LoadBalancer
```

2. Check the status of the service using `kubectl get services` command:
  

```
kubectl get services
```

3. Access your service by navigating to the external IP address of your service in a web browser.
  

## Create with YAML files

To deploy your application in k8s, you can also use `kubectl apply` command. This allows you to create and manage K8s resources, including deployments and services.

You can create a deployment using the following command:

```
kubectl apply -f deployment.yaml
```

Replace `deployment.yaml` with the name of your deployment YAML file.

You can also create a service using the following command:

```
kubectl apply -f service.yaml
```

Replace `service.yaml` with the name of your service YAML file.

