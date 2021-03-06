# gnotifs

> GCP notifications processing using Knative service

GCP exposes many types of events as notifications. You can easy wire these notifications to PubSub of even directly to GCF. However, if you want to send these notifications to external endpoint, like service deployed on Knative, there are few additional steps you will need to take. This demo will walk through the entire process.

## Knative Service

The instructions on building and deploying `gnotifs` service on Knative are located [here](cmd/service/README.md).

## GCP Notifications

Once the GCP notification processing service `gnotifs` is configured on Knative, you will have to set up event individual event sources (triggers). The currently supported GCP notification sources are:

* [Google Cloud Storage (GCS)](pkg/gcs/README.md)
* [Google Drive (Drive)](pkg/drive/README.md)
* Google Assistant (Dialogflow)
* Google Calendar
* Stackdriver

### Demo

The `gnotif` service doesn't do much with the submitted notifications besides output them to log. To demo the incoming notifications you can print these notification logs like this

```shell
kubectl logs -n demo -c user-container -l 'demo=notif'
```

Alternatively, you can stream the logs using [kail](https://github.com/boz/kail).

```shell
kail -l 'demo=notif' -c user-container
```

## Disclaimer

This is my personal project and it does not represent my employer. I take no responsibility for issues caused by this code. I do my best to ensure that everything works, but if something goes wrong, my apologies is all you will get.


