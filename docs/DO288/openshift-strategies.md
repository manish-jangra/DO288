## OpenShift Strategy


#### Custom Deployment Strategies

1. **Rolling**
    The rolling strategy is the default strategy
    This strategy progressively replaces instances of the previous version of an application with instances of the new version of the application. This strategy executes the readiness probe to determine when new pod is ready. After a readiness probe for the new pod succeeds, the deployment controller scales down the old pod.

    If a significant issue occurs, the deployment controller aborts the rolling deployment. Developers can also manually abort the rolling deployment by using the **oc rollout cancel command**

    Rolling deployments in Red Hat OpenShift are canary deployments; Red Hat OpenShift tests a new version (the canary) before replacing all of the old instances. If the readiness probe never succeeds, Red Hat OpenShift removes the canary instance and automatically rolls back the deployment configuration.

    Use a rolling deployment strategy when:
    1. You require no downtime during an application update.
    2. Your application supports running an older version and a newer version at the same time.

2. **Recreate**
    In this strategy, Red Hat OpenShift first stops all the pods that are currently running and only then starts up pods with the new version of the application. This strategy incurs downtime because, for a brief period, no instances of your application are running.
    Use a recreate deployment strategy when:

    1. Your application does not support running an older version and a newer version at the same time.
    2. Your application uses a persistent volume with RWO (ReadWriteOnce) access mode, which does not allow writes from multiple pods.

3. Custom

#### Life-cycle Hooks

The Recreate and Rolling strategies support life-cycle hooks. You can use these hooks to trigger events at predefined points in the deployment process. Red Hat OpenShift deployments contain three life-cycle hooks:

1. **Pre-Lifecycle Hooks**
    Red Hat OpenShift executes the pre-life-cycle hook before any new pods for a deployment start, and also before any older pods shut down
2. **Mid-Lifecycle Hooks**
    The mid-life-cycle hook is executed after all the old pods in a deployment have been shut down, but before any new pods are started. Mid-Lifecycle Hooks are only available for the Recreate strategy
3. **Post-Lifecycle Hooks**
    The post-life-cycle hook is executed after all new pods for a deployment have started, and after all the older pods have shut down


#### Remove triggers from deployment-config
    oc set triggers dc/mysql --from-config --remove

#### Change deployment strategy to Recreate
    oc patch dc/mysql --patch \ 
        '{"spec":{"strategy":{"type":"Recreate"}}}'

#### Remove the rollingParams attribute from deployment config
    oc patch dc/mysql --type=json \
        -p='[{"op":"remove", "path": "/spec/strategy/rollingParams"}]'

#### Rollout the changes manually when triggers are already removed from DeploymentConfig
    oc rollout latest dc/mysql
