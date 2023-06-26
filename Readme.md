## ArgoCD Rollout Learning


1. [Introduction](./01-Introduction/01-Intro.md)
   
   - [Why Argo Rollouts](./01-Introduction/01-Intro.md#why-argo-rollouts)

   - [Overview of Woking](./01-Introduction/02-Working-Overview.md)

2. [Installation & Commands](https://argo-cd.readthedocs.io/en/stable/getting_started/)
   
   - [Install ArgoCD](./02-Installation/Installation.md)
   - [ArgoCD Values Config ](./02-Installation/ArgoCD_Configuration.md)
   - [Install Argo Rollout](./02-Installation/Install-ArgoRollouts.md)
   - [Install ArgoCLI, Argo Rollout plugin](./02-Installation/Install-ArgoCLI.md)

3. **Argo Rollout Workload**
   
   - [Basic Example](./03-Basic-Examples/01-Basic.md)
   - [ALB ingress Example](./03-Basic-Examples/01-ALB-Ingress.md)
   - [Rollout Specitifaction](./03-Basic-Examples/rollspec.yml)

4. [Different Steategy](https://argo-rollouts.readthedocs.io/en/stable/features/bluegreen/)
    
    - [Bluegreen](./04-Strategy/Bluegreen.md)
       - [Sequence of Events](./04-Strategy/Blue-Green-Events.md)
       - [Configurable Feature](./04-Strategy/Configurable-Features.md)
       - [Bluegreen Example](./04-Strategy/BlueGreen-Example.md)