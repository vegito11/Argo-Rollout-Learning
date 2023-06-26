## ArgoCLI 

1. On Macos
   
   ```bash
   $ brew install argoproj/tap/kubectl-argo-rollouts
   ```

   ### Using cURL 
   
   ```bash
   $ curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-darwin-amd64

   $ chmod +x ./kubectl-argo-rollouts-darwin-amd64
   
   $ sudo mv ./kubectl-argo-rollouts-darwin-amd64 /usr/local/bin/kubectl-argo-rollouts
   ```

2. On Linux

   ```bash
   $ curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-linux-amd64

   $ chmod +x ./kubectl-argo-rollouts-linux-amd64
   
   $ sudo mv ./kubectl-argo-rollouts-linux-amd64 /usr/local/bin/kubectl-argo-rollouts
   ```
3. Window
   
   ```Powershell
   $ https://github.com/argoproj/argo-rollouts/releases/download/v1.1.0/kubectl-argo-rollouts-windows-amd64
   ```
-------------------------------------------------------------------------------------

### Verify the Installation

   ```bash
   $ kubectl argo rollouts version
   $ source <(kubectl-argo-rollouts completion bash)
   ```
-------------------------------------------------------------------------------------