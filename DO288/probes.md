## OpenShift (Kubernetes) Probles

1. Startup Probe
2. Readiness Probe
3. Liveness Probe

#### Startup Probe
A startup probe verifies whether the application within a container is started. Startup probes run before any other probe, and, unless it finishes successfully, disables other probes. If a container fails its startup probe, the container is killed and will follow the pod's restartPolicy.

This type of probe is only executed at startup, unlike readiness probes, which are run periodically. The startup probe is configured in the **spec.containers.startupprobe** attribute of the pod configuration.

#### Readiness Probe
Readiness probes determine whether or not a container is ready to serve requests. If the readiness probe returns a failed state, Red Hat OpenShift removes the IP address for the container from the endpoints of all services.

>**trick**
Developers can use readiness probes to signal to Red Hat OpenShift that even though a container is running, it should not receive any traffic from a proxy. This can be useful for waiting for an application to perform network connections, loading files and cache, or generally any initial tasks that might take considerable time and only temporarily affect the application.

#### Liveness Probe
Liveness probes determine whether or not an application running in a container is in a healthy state. If the liveness probe detects an unhealthy state, Red Hat OpenShift kills the container and tries to redeploy it.

The liveness probe is configured in the spec.containers.livenessprobe attribute of the pod configuration

| Name               | Mandatory  | Description                                                                                               | Default Value |
| -------------------| -----------| ----------------------------------------------------------------------------------------------------------|---------------|
| initialDelaySeconds| Yes        | Determines how long to wait after the container starts before beginning the probe.                        |     0         |
| timeoutSeconds     | Yes        | Determines how long to wait for the probe to finish. If this time is exceeded, probe fails.               |     1         |
| periodSeconds      | No         | Specifies the frequency of the checks.                                                                    |     1         |
| successThreshold   | No         | Specifies the minimum consecutive successes for the probe to be considered successful after it has failed.|     1         |
| failureThreshold   | No         | Specifies the minimum consecutive failures for the probe to be considered failed after it has succeeded.  |     3         |