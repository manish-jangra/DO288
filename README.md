# OpenShift

>**Note**
>This github repository is work in progress for OpenShift Certification Exams DO280, DO288 and DO380


👉 How to delete all the pods which are in Error/Failed State or Completed State 
    oc delete pod --field-selector=status.phase==Failed -n namespace
    oc delete pod --field-selector=status.phase==Succeeded -n namespace

👉 Alias your long commands 😊 
    alias gr="oc get -o jsonpath=\’{.spec.host}\’ route " 
    gr routename
    R=$(gr routename)