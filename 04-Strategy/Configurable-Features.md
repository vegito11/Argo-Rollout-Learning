## Configurable Features

1. Fields

    <details>
    <summary> BlueGreen Fields </summary>

      ```yaml
      spec:
       strategy:
          blueGreen:
             autoPromotionEnabled: boolean
             autoPromotionSeconds: *int32
             antiAffinity: object
             previewService: string
             prePromotionAnalysis: object
             postPromotionAnalysis: object
             previewReplicaCount: *int32
             scaleDownDelaySeconds: *int32
             scaleDownDelayRevisionLimit: *int32
      ```
    </details>

2. Spec with Example
   
    <details>
    <summary> BlueGreen Fields </summary>

      ```yaml
          blueGreen:
            # Reference to service that the rollout modifies as the active service.
            # Required.
            activeService: active-service
      
            # Pre-promotion analysis run which performs analysis before the service
            # cutover. +optional
            prePromotionAnalysis:
              templates:
              - templateName: success-rate
              args:
              - name: service-name
                value: guestbook-svc.default.svc.cluster.local
      
            # Post-promotion analysis run which performs analysis after the service
            # cutover. +optional
            postPromotionAnalysis:
              templates:
              - templateName: success-rate
              args:
              - name: service-name
                value: guestbook-svc.default.svc.cluster.local
      
            # Name of the service that the rollout modifies as the preview service.
            # +optional
            previewService: preview-service
      
            # The number of replicas to run under the preview service before the
            # switchover. Once the rollout is resumed the new ReplicaSet will be fully
            # scaled up before the switch occurs +optional
            previewReplicaCount: 1
      
            # Indicates if the rollout should automatically promote the new ReplicaSet
            # to the active service or enter a paused state. If not specified, the
            # default value is true. +optional
            autoPromotionEnabled: false
      
            # Automatically promotes the current ReplicaSet to active after the
            # specified pause delay in seconds after the ReplicaSet becomes ready.
            # If omitted, the Rollout enters and remains in a paused state until
            # manually resumed by resetting spec.Paused to false. +optional
            autoPromotionSeconds: 30
      
            # Adds a delay before scaling down the previous ReplicaSet. If omitted,
            # the Rollout waits 30 seconds before scaling down the previous ReplicaSet.
            # A minimum of 30 seconds is recommended to ensure IP table propagation
            # across the nodes in a cluster.
            scaleDownDelaySeconds: 30
      
            # Limits the number of old RS that can run at once before getting scaled
            # down. Defaults to nil
            scaleDownDelayRevisionLimit: 2
      
            # Add a delay in second before scaling down the preview replicaset
            # if update is aborted. 0 means not to scale down. Default is 30 second
            abortScaleDownDelaySeconds: 30
      
            # Anti Affinity configuration between desired and previous ReplicaSet.
            # Only one must be specified
            antiAffinity:
              requiredDuringSchedulingIgnoredDuringExecution: {}
              preferredDuringSchedulingIgnoredDuringExecution:
                weight: 1 # Between 1 - 100
      ```

----------------------------

1. `autoPromotionEnabled`:
   - This field determines whether the rollout automatically promotes the new ReplicaSet to the active service once it's healthy.
   - Example: If `autoPromotionEnabled` is set to `true` (default), the new ReplicaSet will be automatically promoted.

2. `autoPromotionSeconds`:
   - This field specifies the time in seconds after which the rollout automatically promotes the new ReplicaSet to the active service.
   - Example: If `autoPromotionEnabled` is set to `true` and `autoPromotionSeconds` is set to 60, the new ReplicaSet will be promoted after 60 seconds.

3. `antiAffinity`:
   - This field is used to configure anti-affinity rules, which control how pods are scheduled on different nodes to avoid running multiple pods on the same node.
   - Example: If `antiAffinity` is specified, it ensures that pods from the same ReplicaSet are not scheduled on the same node.

4. `prePromotionAnalysis`:
   - This field allows for configuring an analysis run before switching traffic to the new version.
   - Example: If `prePromotionAnalysis` is set, the rollout will wait for the analysis run to finish successfully before switching traffic to the new ReplicaSet.

5. `postPromotionAnalysis`:
   - This field configures an analysis run after the traffic is switched to the new version.
   - Example: If `postPromotionAnalysis` is set and the analysis run fails, the rollout will switch traffic back to the previous stable ReplicaSet.

6. `previewService`:
   - This field references a Service that sends traffic to the new ReplicaSet before it's promoted to receive traffic from the active service.
   - Example: If `previewService` is specified, the Service will direct traffic to the new ReplicaSet for testing purposes.

7. `previewReplicaCount`:
   - This field indicates the number of replicas for the new version during the preview phase.
   - Example: If `previewReplicaCount` is set to 2, the new ReplicaSet will run with 2 replicas during testing before being promoted.

8. `scaleDownDelaySeconds`:
   - This field specifies the delay in seconds before scaling down the old ReplicaSet after switching the active service to the new ReplicaSet.
   - Example: If `scaleDownDelaySeconds` is set to 30 (default), the old ReplicaSet will be scaled down after a 30-second delay.

9. `scaleDownDelayRevisionLimit`:
   - This field limits the number of old active ReplicaSets to keep scaled up while they wait for the scaleDownDelay to pass after being removed from the active service.
   - Example: If `scaleDownDelayRevisionLimit` is set to 2, only the two most recent old ReplicaSets will be retained for the specified scaleDownDelay.

These fields provide configuration options for fine-tuning the blue-green update strategy, allowing for automatic promotion, analysis runs, previewing the new version, controlling scaling, and managing the transition from the old to the new ReplicaSets.