# Matrix Sliding Sync helm chart

<a href="https://github.com/small-hack/matrix-sliding-sync-chart/releases"><img src="https://img.shields.io/github/v/release/small-hack/matrix-sliding-sync-chart?style=plastic&labelColor=blue&color=green&logo=GitHub&logoColor=white"></a>

This is a helm chart implementing [matrix-org/sliding-sync](https://github.com/matrix-org/sliding-sync/tree/main) for deployment on Kubernetes. It was originally designed for use as a subchart for [small-hack/matrix-chart](https://github.com/small-hack/matrix-chart), but it can be used stand alone as well.

See the [`README.md`](https://github.com/small-hack/matrix-sliding-sync-chart/blob/main/charts/matrix-sliding-sync/README.md) for docs auto-generated from the [`values.yaml`](https://github.com/small-hack/matrix-sliding-sync-chart/blob/main/charts/matrix-sliding-sync/values.yaml).

Read through the parameters and modify them locally before installing the chart:

```bash
# add the helm repo locally
helm repo add matrix-sliding-sync https://small-hack.github.io/matrix-sliding-sync-chart

# downloads the values.yaml locally
helm show values matrix-sliding-sync/matrix-sliding-sync > values.yaml

# install the chart
helm install my-release-name matrix-sliding-sync/matrix-sliding-sync --values values.yaml
```

## Status

Not yet functional. Tests still not passing. If you know why, please submit PR.
