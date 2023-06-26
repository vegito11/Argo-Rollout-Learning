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

## Field List

- [Active Service](#active-service)
- [Pre-Promotion Analysis](#pre-promotion-analysis)
- [Post-Promotion Analysis](#post-promotion-analysis)
- [Preview Service](#preview-service)
- [Preview Replica Count](#preview-replica-count)
- [Auto Promotion](#auto-promotion)
- [Auto Promotion Seconds](#auto-promotion-seconds)
- [Scale Down Delay](#scale-down-delay)
- [Scale Down Delay Revision Limit](#scale-down-delay-revision-limit)
- [Abort Scale Down Delay](#abort-scale-down-delay)
- [Anti-Affinity](#anti-affinity)

----------------------------------

## Active Service

  - The `activeService` field references the service that the rollout modifies as the active service. This service is responsible for handling incoming traffic.

    ```yaml
    blueGreen:
    activeService: active-service
    ```
     In the above example, the active service is set to `active-service`.
  
----------------------------------

## Pre-Promotion Analysis

   - The `prePromotionAnalysis` field allows for performing analysis before the service cutover. 

   - This analysis run can be used to `validate the readiness` of the new ReplicaSet before switching traffic to it.

     ```yaml
     blueGreen:
       prePromotionAnalysis:
         templates:
         - templateName: success-rate
           args:
           - name: service-name
             value: guestbook-svc.default.svc.cluster.local
     ```

   - In the above example, a pre-promotion analysis is configured using the "success-rate" template. 

   - It takes an argument `service-name` with a value of "guestbook-svc.default.svc.cluster.local".

----------------------------------

## Post-Promotion Analysis

  - The `postPromotionAnalysis` field allows for performing analysis after the service cutover. This analysis run can be used to `verify the stability and performance` of the new ReplicaSet.


     ```yaml
     blueGreen:
       postPromotionAnalysis:
         templates:
         - templateName: success-rate
           args:
           - name: service-name
             value: guestbook-svc.default.svc.cluster.local
     ```
   
   - In the above example, a post-promotion analysis is configured using the "success-rate" template.   
   - It takes an argument `service-name` with a value of "guestbook-svc.default.svc.cluster.local".

----------------------------------

## Preview Service

   - The `previewService` field specifies the name of the service that the rollout modifies as the preview service.   
   - This service allows for testing the new version of the application before promoting it to the active service.


     ```yaml
     blueGreen:
       previewService: preview-service
     ```
    
     In the above example, the preview service is set to `preview-service`.

----------------------------------

## Preview Replica Count

   - The `previewReplicaCount` field indicates the number of replicas to run under the preview service before the switchover. 

   - It allows for testing the new ReplicaSet with a smaller number of replicas.

        ```yaml
        blueGreen:
           previewReplicaCount: 1
        ```
   
   - In the above example, the preview ReplicaSet is configured to have 1 replica.

----------------------------------

## Auto Promotion

  - The `autoPromotionEnabled` field determines whether the rollout should automatically promote the new ReplicaSet to the active service or enter a paused state.  
  
  -  If not specified, the default value is `true`.

        ```yaml
        blueGreen:
          autoPromotionEnabled: false
        ```
   - In the above example, the rollout will enter a paused
     state instead of automatically promoting the new ReplicaSet.

----------------------------------

## Auto Promotion Seconds

   - The `autoPromotionSeconds` field automatically promotes the current ReplicaSet to active after the specified pause delay in seconds.   
   - If omitted, the rollout remains in a paused state until manually resumed.

        ```yaml
        blueGreen:
          autoPromotionSeconds: 30
        ```
   - In the above example, the rollout will automatically promote the new ReplicaSet to active after a pause delay of 30 seconds.

----------------------------------

## Scale Down Delay

   - The `scaleDownDelaySeconds` field adds a delay before scaling down the previous ReplicaSet.  

   - This delay ensures proper IP table propagation across the nodes in a cluster. If omitted, the default delay is 30 seconds.

        ```yaml
        blueGreen:
          scaleDownDelaySeconds: 30
        ```
   - In the above example, a delay of 30 seconds is added before scaling down the previous ReplicaSet.

----------------------------------

## Scale Down Delay Revision Limit

  - The `scaleDownDelayRevisionLimit` field limits the number of old ReplicaSets that can run at once before being scaled down.  

  - If omitted, all ReplicaSets will be retained during the scale-down delay.

    ```yaml
    blueGreen:
      scaleDownDelayRevisionLimit: 2
    ```
  - In the above example, a maximum of 2 old ReplicaSets will be allowed to run during the scale-down delay.

----------------------------------

## Abort Scale Down Delay

   - The `abortScaleDownDelaySeconds` field adds a delay in seconds before scaling down the preview ReplicaSet if the update is aborted.   

   - If set to 0, no scale-down delay will be applied. The default value is 30 seconds.

     ```yaml
     blueGreen:
       abortScaleDownDelaySeconds: 30
     ```
   
   - In the above example, a delay of 30 seconds is added before scaling down the preview ReplicaSet in case of an update abortion.

----------------------------------

## Anti-Affinity

   - The `antiAffinity` field configures the anti-affinity rules between the desired and previous  ReplicaSets. Only one type of anti-affinity can be specified.


     ```yaml
     blueGreen:
       antiAffinity:
         requiredDuringSchedulingIgnoredDuringExecution: {}
         preferredDuringSchedulingIgnoredDuringExecution:
           weight: 1
     ```
   
   - In the above example, anti-affinity is configured using `preferredDuringSchedulingIgnoredDuringExecution` with a weight of 1, indicating a preference to avoid scheduling the desired and previous ReplicaSets on the same node if possible.

----------------------------------