## OpenShift Strategy


#### Custom Deployment Strategies

1. Rolling
2. Recreate
3. Custom

#### Life-cycle Hooks

The Recreate and Rolling strategies support life-cycle hooks. You can use these hooks to trigger events at predefined points in the deployment process. Red Hat OpenShift deployments contain three life-cycle hooks:

1. Pre-Lifecycle Hooks
    Red Hat OpenShift executes the pre-life-cycle hook before any new pods for a deployment start, and also before any older pods shut down
2. Mid-Lifecycle Hooks
    The mid-life-cycle hook is executed after all the old pods in a deployment have been shut down, but before any new pods are started. Mid-Lifecycle Hooks are only available for the Recreate strategy
3. Post-Lifecycle Hooks
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
