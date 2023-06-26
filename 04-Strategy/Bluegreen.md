## BlueGreenUpdate Strategy Explanation:

- When deploying new versions of an application using Argo Rollouts, the BlueGreenUpdate strategy helps ensure  
 a smooth transition from the old version to the new version.  
  It involves two main steps:

   1. Active and Preview Services:
     
     - An `"Active Service"` is responsible for sending regular traffic to the **old version** of the application.

     - A "`Preview Service"` is used to direct traffic to the **new version** of the application.

   2. Rollout Process:

      - When a change is made to the application's configuration, Argo Rollouts creates a new ReplicaSet (a group of pods representing the application).

      - If the Active Service is not currently directing traffic to any ReplicaSet, Argo Rollouts immediately starts sending traffic to the new ReplicaSet.

      - If the Active Service is already pointing to a ReplicaSet, it continues to do so while the new ReplicaSet becomes available.

      - Once the new ReplicaSet is ready, Argo Rollouts `modifies the Active Service` to start directing traffic to the new ReplicaSet.
      
      - After a specified time (configured by `scaleDownDelaySeconds`), Argo Rollouts `scales down` the old ReplicaSet, removing it from the deployment.

--------------------------------------------------------------------

## Example:

- Let's consider an example of a website called "MyWebsite" using BlueGreenUpdate strategy:

   1. Active Service: `mywebsite-active`
     
      - This service currently directs traffic to the old version of the website.

   2. Preview Service: `mywebsite-preview`
     
      - This service is used to send traffic to the new version of the website.

   3. Rollout Process:

      - Initially, the Active Service points to ReplicaSet `A`, representing the old version of the website.

      - When a new version of the website is deployed, Argo Rollouts creates ReplicaSet `B` for the new version.

      - If the Active Service is not directing traffic to any ReplicaSet, Argo Rollouts immediately starts sending traffic to ReplicaSet `B`.

      - If the Active Service is already pointing to ReplicaSet `A`, it continues to do so while ReplicaSet `B` becomes available.

      - Once ReplicaSet `B` is ready, Argo Rollouts modifies the Active Service to point to ReplicaSet `B`, directing traffic to the new version.
     
      - After a specified time (e.g., 30 seconds), Argo Rollouts scales down ReplicaSet `A`, removing the old version of the website.

   By using the BlueGreenUpdate strategy, Argo Rollouts ensures that there is minimal downtime and a seamless transition from the old version to the new version of the website.

--------------------------------------------------------------------

[Next - Blue Green Events](./Blue-Green-Events.md)