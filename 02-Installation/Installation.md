## Prerequisites

- Kubernetes cluster
- Helm v3
- Kubectl

------------------

## 1. Using Kubectl
   
   ```bash
   $ kubectl create namespace argocd
   $ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```
------------------

## 2. Installing ArgoCD with Helm 

   1. Add the ArgoCD Helm repository:

       ```bash
       $ helm repo add argo https://argoproj.github.io/argo-helm
       ```

  2. Update the Helm repositories:
   
     ```bash
     $ helm repo update
     ```

  3. Create a namespace for ArgoCD:
   
     ```bash
     $ kubectl create namespace argocd
     ```

  4. Install ArgoCD using Helm:
   
     ```bash
     $ helm install argocd argo/argo-cd -n argocd
     ```
   
   5. Or install using values

       ```bash
       $ helm pull argo/argo-cd
       $ tar -xvf argo-cd*.tgz && rm argo-cd*.tgz
       $ helm dependency up
       $ helm install -n argocd argocd  --values values-development.yaml  . 
       ```


------------------

## Verify the Installation

  1. See the Pods
   
     ```bash
     $ kubectl get pods -n argocd
     ```

     Ensure that all the ArgoCD pods are in a running state.

  2. Access the ArgoCD web UI:
   
     ```bash
     $ kubectl port-forward svc/argocd-server -n argocd 8080:443

     # If you want to access from other machines
     $ kubectl port-forward svc/argocd-server -n argocd 8080:443 --address="0.0.0.0'
     ```

   3. Open your web browser and navigate to `http://localhost:8080`. 
   
   4. Use the default username `admin` and retrieve the password:
   
      ```bash
      $ kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
      ```
    
   > (You should delete the initial secret afterwards as suggested by the [Getting Started Guide](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

   ```bash
   $ argocd account update-password 
   ```

------------------

## CleanUp

  1. Clean up (optional):
   
     ```shell
     $ helm uninstall argocd -n argocd
     ```
  
  2. Remove the associated CRDs
    
     ```bash
     $ kubectl delete crd applications.argoproj.io

     $ kubectl delete crd appprojects.argoproj.io
     ```

     This will uninstall ArgoCD from your cluster.

------------------

