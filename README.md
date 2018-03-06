# project
Design docs and Issue tracker for this Project

## What is Prohori

**Prohori** (_Praharī_) - (প্রহরী in Bangla) means watchman in English. In this project, Prohori is a watchman for Kubernetes objecrs.

Prohori is a part-time hobby project inspired by [searchlight](https://github.com/appscode/searchlight). Unlike searchlight, Prohori implementation design does not require Icinga and Database. And this limitation makes it lightweight and usable only for dev cluster.

Prohori will use [plugins](https://github.com/appscode/searchlight/tree/master/plugins) supported by searchlight to check Kubernetes objects and [go-notify](https://github.com/appscode/go-notify) to send notifications.

Instead of Icinga, Prohori will use Cron by [robfig](https://github.com/robfig/cron) to run checker periodically.

### Prohori may be support following features:

- [ ] Single Resource Type for checker.
- [ ] Add external plugin anytime on Running Kucker.
- [ ] Track command State (count) and notification (count) in Status.
- [ ] Single Resource type for notification.
- [ ] Edit notification Resource object to acknowledge.

### Limitation of Prohori:

- [ ] Doesn't have any UI.
- [ ] It may not function with high load.
- [ ] Restarting controller will start cron from zero.
- [ ] And all cool features supported by Icinga.

## What might Alerta object look like?

Alerta is catalan of Alert - [GT](https://translate.google.com/#auto/ca/alert).

```yaml
apiVersion: monitoring.prohori/v1alpha1
kind: Alerta
metadata:
  name: pod-status
spec:
  type: PodAlert
  command: pod_status
  flags:
  - --key1=val1
  - --key2=val2
  selector:
    namespace: demo
    matchLabels:
      app: nginx
  plugin:
    pullBinaryPolicy: IfNotPresent
    binary: https://github.com/kucker/plugin/releases/download/v0.1.0/pod_status
  checkInterval: 30s
  alertInterval: 2m
  notifierSecretName: notifier-config
  receivers:
  - notifier: Mailgun
    state: CRITICAL
    to: ["ops@example.com"]
```

Here,
 - `spec.type` can be PodAlert, NodeAlert, ClusterAlert.
 - Prohori will execute `pod_status` command with provided arguments. 
 - `spec.selector` will specify for which Pods this check will be done.
 - `spec.plugin` holds necessary information to download on-the-fly external binary.
