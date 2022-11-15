# Replicated vendor portal app manifest files to show multiple instances of same helm chart
Manifest files for the replicated vendor portal to deploy the same helm chart twice in same app.

Note the application fragment here shows use of subdirectories to separate the files logically, this is useful when the application has many sub-components.

The gh-nginx-helm directory contains the *gh-nginx-helm* helm chart which was created using helm cli, helm create and then tweaked slightly to change the auto-generated names.

The packaged helm chart tgz is placed in the manifests/helmcharts directory and two instances of the helm chart defined using the replicated kots.io HelmChart CRD:

manifests/gh-helm-app/kots-gh-helm-app.yaml
```
apiVersion: kots.io/v1beta1
kind: HelmChart
metadata:
  name: gh-helm-app
spec:
  # chart identifies a matching chart from a .tgz
  chart:
    name: gh-nginx-helm
    chartVersion: "0.1.0"
    releaseName: gh-helm-app
```

manifests/gh-helm-app2/kots-gh-helm-app2.yaml
```
apiVersion: kots.io/v1beta1
kind: HelmChart
metadata:
  name: gh-helm-app2
spec:
  # chart identifies a matching chart from a .tgz
  chart:
    name: gh-nginx-helm
    chartVersion: "0.1.0"
    releaseName: gh-helm-app2
```

The key parameter used here is the [spec.chart.releaseName](https://docs.replicated.com/reference/custom-resource-helmchart#chartreleasename)

