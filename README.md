# project
Design docs and Issue tracker for this Project

## What is Kucker

Kucker is a Kubernetes objects Checker controller. This idea is moving around in my head for a long time. 

Kucker is a part-time hobby project inspired by [searchlight](https://github.com/appscode/searchlight). Unlike searchlight, Kucker implementation design does not require Icinga and Database. And this limitation makes it lightweight and usable only for dev cluster.

Kucker will use [plugins](https://github.com/appscode/searchlight/tree/master/plugins) supported by searchlight to check Kubernetes objects and [go-notify](https://github.com/appscode/go-notify) to send notifications.

Instead of Icinga, Kucker will use Cron by [robfig](https://github.com/robfig/cron) to run checker periodically.

### Kucker may be support following features:

- [ ] Single Resource Type for checker.
- [ ] Add external plugin anytime on Running Kucker.
- [ ] Track command State (count) and notification (count) in Status.
- [ ] Single Resource type for notification.
- [ ] Edit notification Resource object to acknowledge.

### Limitation of Kucker:

- [ ] Doesn't have any UI.
- [ ] It may not function with high load.
- [ ] Restarting controller will start cron from zero.
- [ ] And all cool features supported by Icinga.
