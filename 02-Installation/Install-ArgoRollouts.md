## Prerequisites

- Kubernetes cluster
- Helm v3
- Kubectl

------------------

## 1. Using Kubectl
   
   ```bash
   kubectl create namespace argo-rollouts
   kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
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
     $ kubectl create namespace argo-rollouts
     ```

  4. Install ArgoCD using Helm:
   
     ```bash
     $ helm install argo-rollouts argo/argo-rollouts -n argocd
     ```
   
   5. Or install using values

       ```bash
       $ helm pull argo/argo-rollouts
       $ tar -xvf argo-rollouts*.tgz && rm argo-rollouts*.tgz
       $ helm dependency up
       $ helm install -n argo-rollouts argo-rollouts  --values values-development.yaml  . 
       ```


------------------


