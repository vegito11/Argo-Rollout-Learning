# Argo Rollouts Documentation

## Introduction

   - Argo Rollouts is a powerful Kubernetes controller and a set of custom resource definitions (CRDs) that `enhance deployment capabilities` in Kubernetes.   
   
   - It offers advanced features like blue-green deployments, canary deployments, canary analysis, experimentation, and progressive delivery.

   - Argo Rollouts **integrates** with popular `ingress controllers` and `service meshes`, leveraging their traffic shaping capabilities to gradually shift traffic to new versions during updates.  
   
   -  It also `supports querying and interpreting metrics` from various providers to validate key performance indicators (KPIs) and drive automated promotion or rollback actions during updates.

------------------------------------------------------------------------------------------

## Why Argo Rollouts?

  - While the native Kubernetes Deployment Object provides the RollingUpdate strategy for basic safety guarantees during updates, it has certain limitations:

    1. Limited control over the rollout speed.

    2. Inability to control traffic flow to the new version.

    3. Readiness probes are not suitable for deeper, stress, or one-time checks.

    4. No ability to query external metrics to verify an update.

    5. Inability to automatically abort and rollback the update in case of failures.


  - In large-scale, `high-volume` production environments, a rolling update is often considered too risky due to its lack of control over the blast radius, 
   aggressive rollout behavior, and absence of automated rollback mechanisms.

------------------------------------------------------------------------------------------

## Argo Rollouts Controller Features

  - Argo Rollouts provides the following features to overcome the limitations of the native Kubernetes Deployment Object:

  1. **Blue-Green Update Strategy**

     - With the blue-green update strategy, Argo Rollouts allows you to deploy **new versions** `alongside the existing version` and then switch traffic from the old version to the new version seamlessly.  

     ---------------------------------------------

  1. **Canary Update Strategy**

     - The canary update strategy enables you to roll out **new versions** to a `small subset` of users or traffic and gradually increase the exposure to monitor and validate the new version's performance before full rollout.

     ---------------------------------------------
  
  1. **Fine-Grained, Weighted Traffic Shifting**

     - Argo Rollouts offers fine-grained control over traffic shifting by allowing you to specify weights for different versions. This enables you to `gradually shift traffic` from one version to another based on your defined criteria.

     ---------------------------------------------
  
  1. **Automated Rollbacks and Promotions**

     - In case of failures or unexpected issues, Argo Rollouts `automatically rolls back to the previous version`, ensuring that your applications remain stable and available. It also supports automated promotions when a new version passes validation criteria.
     
     ---------------------------------------------

  1. **Manual Judgement**

     - Argo Rollouts provides the ability to incorporate manual approval steps in the deployment process. This allows human intervention to verify the new version's functionality or perform additional checks before proceeding with the rollout.

     ---------------------------------------------

  1. **Ingress Controller and Service Mesh Integration**

     - Argo Rollouts seamlessly integrates with popular ingress controllers like NGINX, ALB, Apache APISIX, and service meshes like Istio, Linkerd, and SMI. This integration leverages the traffic shaping capabilities of these tools to control traffic flow during updates.

     ---------------------------------------------

  1. **Simultaneous Usage of Multiple Providers**

     - You can use Argo Rollouts with multiple providers simultaneously, such as combining SMI with NGINX or Istio with ALB, allowing you to leverage the strengths of different tools for traffic management.

     ---------------------------------------------

  1. **Metric Provider Integration**

     - Argo Rollouts supports integration with various metric providers like Prometheus, Wavefront, Kayenta, Web, Kubernetes Jobs, Datadog, New Relic, Graphite, and InfluxDB. This integration enables you to query and analyze business KPIs during the rollout process.

     ---------------------------------------------
    
   - By leveraging these features, Argo Rollouts empowers you to perform controlled, automated, and sophisticated deployments in Kubernetes,   
    mitigating risks and ensuring smooth updates for your applications.

---------------------------------------------

For detailed documentation and usage instructions, please refer to the [official Argo Rollouts documentation](https://argoproj.github.io/argo-rollouts/).