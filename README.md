# Deploying three application and access it through nginx-ingress

### 1. Clone the repository
    $ git https://github.com/paawanyadav/kubernetes_wordpress-mysql.git
    $ cd wordpress

### 2. Configure password for DB or leave it default 
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
