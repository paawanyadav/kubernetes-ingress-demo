# Deploying three application and access it through nginx-ingress

### 1. Clone the repository
    $ git clone https://github.com/paawanyadav/kubernetes-ingress-demo.git
    $ cd kubernetes-ingress-demo
    
### 2. Pre-requisite
    -- Ingress need Loadbalancer 
    -- I'm using metallb, is a load-balancer implementation for bare metal Kubernetes clusters
    -- Just copy these commands for adding Metallb in your cluster
    
    $ kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/namespace.yaml
    $ kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/metallb.yaml
    
    -- In metallb-config.yaml file reserve some IP for metallb as per your node IP's
    $ kubectl apply -f metallb-config.yaml

### 3. Now apply yaml files in series
    # Run Below Command Step by Step
    -- Mysql 
    $ kubectl apply -f mysql/mysql-secret.yaml
    $ kubectl apply -f mysql/mysql.yaml
    
    -- Wordpress
    $ kubectl apply -f wordpress/db-connection-configmap.yaml
    $ kubectl apply -f wordpress/wordpress.yaml
    $ kubectl apply -f wordpress/wordpress-service.yaml
    
    -- Node Application
    $ kubectl apply -f nodeapp/nodeapp-deployment.yaml
    $ kubectl apply -f nodeapp/nodeapp-service.yaml
    
    -- Dotnet Application
    $ kubectl apply -f asp-app/aspnewer-deployment.yaml
    $ kubectl apply -f asp-app/aspnewer-service.yaml
    
    -- Ingress
    $ kubectl apply -f ingress.yaml
    
### 3. Check your LoadBalancer Port  
    $ kubectl get ingress personal-ingress
    -- Copy "IP" mentioned in "Address" column

### 4. Setup local DNS entry 
    $ sudo nano /etc/host
    -- paste Ip wordpress.example.com  EX- 172.16.16.151 wordpress.example.com
    -- paste Ip aspnewer.example.com   EX- 172.16.16.151 aspnewer.example.com
    
### 5. All Done!!
    -- Now You can access your sites
    -- Wordpress  ---> wordpress.example.com
    -- Node App   ---> wordpress.example.com/node
    -- Dotnet App ---> aspnewer.example.com

### 6. Importannt Commands
    -- kubectl cluster-info      --> Give Cluster information
    -- kubectl get all -o wide   --> Detailed information about on going process
    -- kubectl get deploy        --> Give details of deployment
    -- kubectl get services      --> Give details of services
    -- kubectl get pods          --> Give details of pods
    -- kubectl describe "object" --> Give detailed information

### Important Links 
[metallb](https://metallb.universe.tf/installation/)
[Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
[Nginx-Ingress](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/)
