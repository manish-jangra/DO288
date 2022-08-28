## OpenShift Strategy


#### Custom Deployment Strategies

1. Rolling
2. Recreate
3. Custom

#### Life-cycle Hooks

1. Pre-Lifecycle Hooks
2. Mid-Lifecycle Hooks
3. Post-Lifecycle Hooks


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
    