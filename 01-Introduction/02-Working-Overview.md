## How does it work?

 - Argo Rollouts operates by managing ReplicaSets, similar to the native Kubernetes Deployment Object. 
 -  The controller handles the creation, scaling, and deletion of ReplicaSets based on the specifications defined in the Rollout resource.

  - Here's an overview of the process:

  
1. **Specifying the template**: 
     
     - The Rollout resource includes a `spec.template` field, which contains the pod template that will be used by the ReplicaSets.  

     - This template is the same as the one used in the deployment object.

2. **Introducing a new ReplicaSet**: 
   
   - When a change is made to the `spec.template`, it indicates the introduction of a new ReplicaSet.   
   
   - The Argo Rollouts controller detects this change and initiates the rollout process.

3. **Rollout strategy**: 
   
   - The rollout strategy is defined in the `spec.strategy` field. 

   - It determines how the rollout will progress from the old ReplicaSet to the new ReplicaSet. 

   - Argo Rollouts supports various strategies such as blue-green, canary, and more.

4. **Scaling up the new ReplicaSet**: 
   
   - Once the new ReplicaSet is created, the controller scales it up by gradually increasing the number of replicas.   

   - This can be controlled based on configurable parameters such as the maximum surge or the number of parallel pods.

5. **Analysis (optional)**: 
   
   - Argo Rollouts provides the option to perform analysis on the new ReplicaSet before marking it as "stable."  
   
   - This analysis can involve validating metrics, running tests, or checking custom conditions.   
   
   - If the analysis passes, the ReplicaSet is considered stable and ready for traffic.

6. **Transition to the new ReplicaSet**: 
   
   - With the new ReplicaSet marked as stable, the controller directs traffic to it, gradually shifting traffic away from the old ReplicaSet.   

   - This can be achieved by integrating with ingress controllers or service meshes that handle traffic routing.

7. **Updating the template during rollout**: 
   
   - If there are further changes to the `spec.template` while transitioning from a stable ReplicaSet to a new one (e.g., updating the application version), the previously new ReplicaSet is scaled down.  
   
   -  The controller then progresses to the ReplicaSet reflecting the updated template, ensuring the rollout aligns with the latest changes.
  
       --------------------------

  - Argo Rollouts offers different strategies and behaviors to provide advanced deployment capabilities, allowing you to safely   
   and effectively manage the rollout of your applications in Kubernetes.  

     By leveraging ReplicaSets and controlled traffic shifting, Argo Rollouts enables progressive delivery and canary analysis to ensure successful updates and minimize the risk of failures.