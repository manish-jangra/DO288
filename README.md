# OpenShift

>**Note**
>This github repository is work in progress for OpenShift Certification Exams DO280, DO288 and DO380


#### 👉 How to delete all the pods which are in Error/Failed State or Completed State 
    oc delete pod --field-selector=status.phase==Failed -n namespace
    oc delete pod --field-selector=status.phase==Succeeded -n namespace

#### 👉 Alias your long commands 😊 
    alias gr="oc get -o jsonpath=\’{.spec.host}\’ route " 
    gr routename
    R=$(gr routename)

#### 👉 Filter logs selectively --> e.g display line and a line after the match occres
    oc describe deployment deployment-name | grep -i -A 1 liveness

This will display a line that incluness liveness or Liveness (-i for remove case sensivity) and a line after.

#### 👉 Display rollout history
    oc rollout history deploymentconfig/deployment-name
    oc rollout history deploymentconfig/deployment-name --revision=1
    oc rollback dc/dc-name    # Last Sucessful Version

#### 👉 How to use jq
    oc get dc/hello1 -o json | jq 'spec.template.spec.containers[0].image'

    oc patch pv/cmf-logs-dev -p '{"spec":{"claimRef": null}}'

#### Allow to use image stream from another project
    oc policy add-role-to-group -n project system:image-puller system:serviceaccounts:project-name
    
#### Gracefully restart the cluster nodes
    oc adm cordon <node-name>
    oc adm drain <node-name> --ignore-daemonsets=true --delete-emptydir-data=true --force
#### Test Map
      ------------------------
      |          |           |
      |   Bed    |  Living   |
      |   Room   |   Room    |
      |          |           |
      |----------|-----------|
      |          |           |
      |  Kitchen |  Dining   |
      |          |   Room    |
      ------------------------

https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
