## Architecture

```yml
localhost -> state store <- operators -> resources
```

- applications are grouped by namespaces;
- applications are managed by namespaces;
- pod per container;
- pod is managed by label;
- pod per container, containers are managed by namespaces;

## Configuration

### Globals

> `~/.kube/config`

```yml
apiVersion: v1
clusters:
  - cluster:
      certificate-authority: /home/darius/.minikube/ca.crt
      server: https://192.168.39.48:8443
    name: minikube
contexts:
  - context:
      cluster: minikube
      user: minikube
    name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
  - name: minikube
    user:
      client-certificate: /home/darius/.minikube/client.crt
      client-key: /home/darius/.minikube/client.key
```

### Namespace

```yml
apiVersion: v1
kind: Namespace
metadata:
  name: workshop
```

### POD

```yml
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  namespace: workshop
  labels:
    app: tomcat
spec:
  containers:
    - name: tomcat
      image: tomcat:9
```

### Service

> [docs](https://kubernetes.io/docs/concepts/services-networking/service/)

- clusterip
- nodeport
- load balancer

```yml
apiVersion: v1
kind: Service
metadata:
  name: tomcat
  namespace: workshop
spec:
  type: NodePort  
  selector: 
    app: tomcat
  ports:
    - name: http
      protocol: TCP  
      port: 8080
```

### Deployment

> [docs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tonda100-deployment
  namespace: workshop
  labels:
    app: tonda100
spec:
  replicas: 3
  selector:
    matchLabels:
      app: tonda100
  template:
    metadata:
      name: tonda100
      labels:
        app: tonda100
    spec:
      containers:
      - name: tonda100
        image: tonda100/dummy-app:1
        ports:
        - containerPort: 8080
        resources:
          requests:
            memory: "1Gi"
          limits: 
            memory: "2Gi"
        readinessProbe:   
          httpGet: 
            path: /info
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 3
```

#### Util script
`while sleep 1; do curl http://localhost:30240/info && echo ""; done`

#### Resources

- Memory requests: minimal memory
- Memory limits: if more than kubernetes will kill it
- compiled java8, runtime java11

#### Probes

> [docs](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

- liveness
  - should restart container?
- readiness
  - is application ready?

## Kubernetes solutions

- [ helm ](https://github.com/helm/helm)
- [ HashiCorp ](https://www.hashicorp.com/) 
- [ kubeadm/kops/rancher ](https://rancher.com)

## Basic commands

- `kubectl version`
- `kubectl create namespace <name>`
- `kubectl get namespace <name> -o yaml`
- `kubectl get namespaces`
- `kubectl create -f namespace.yml`
- `kubectl apply -f namespace.yml`
- `kubectl apply -f pod.yml`
- `kubectl -n <namespace name> get pods`
- `kubectl -n <namespace name> describe pod tomcat`
- `kubectl get services`
- `kubectl -n <namespace name> logs`
- `kubectl describe node minikube`
- `kubectl delete namespace <namespace name>`
