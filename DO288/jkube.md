```xml
<properties>
    <jkube.build.switchToDeployment>true</jkube.build.switchToDeployment>
</properties>
```

```xml
<plugin>
    <groupId>org.eclipse.jkube</groupId>
    <artifactId>openshift-maven-plugin</artifactId>
    <version>1.2.0</version>
</plugin>
```

OpemShift Menifests Files: src/main/jkube

Jkube generated OpenShift Files: target/classes/META-INF/jkube/openshift

Jkube generated OpenShift Combine file: target/classes/META-INF/jkube/openshift.yaml

MYSQL_DB=$(echo mysql.ocp-${RHT_OCP4_WILDCARD_DOMAIN#"apps."})