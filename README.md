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
    
    
    
    
### 3. Now apply yaml files in series  
    => Before make changes in mysql-secret.yaml encode your values
    $ For Encode --> echo -n "Yourvalue" | base64
    $ For Decode --> echo -n "EncodedValue" | base64 -d
    $ nano mysql-secret.yaml

### 3. Apply files 
    $ kubectl apply -f mysql-secret.yaml
    $ kubectl apply -f mysql.yaml
    $ kubectl db-connection-configmap.yaml
    $ kubectl wordpress.yaml

### 5. By Using NodePort
    -- Uncomment line 53 and 60 in file wordpress.yaml
    -- Again Follow Apply files 
    -- kubectl get all -o wide --> by this see where your wordpress is running in which node 
    -- Hit node IP with NodePort 30080  --> IP:30080

### 6. Importannt Commands
    -- kubectl cluster-info  --> Give Cluster information
    -- kubectl get all -o wide  --> Detailed information about on going process
    -- kubectl get deploy  --> Give details of deployment
    -- kubectl get services --> Give details of services
    -- kubectl get pods --> Give details of pods
    -- kubectl describe "pod-name" , "service-name" --> Give detailed information
