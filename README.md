# NOTICE OF ARCHIVAL

Looks like the sliding sync proxy is being deprecated according to the matrix org:

> We will be decommissioning the [sliding sync proxy](https://github.com/matrix-org/matrix-spec-proposals/pull/3575) next week (21/11/2024) and Element are removing client support in mid-January (17/01/2025).

You can learn more in this [matrix blog post](https://matrix.org/blog/2024/11/14/moving-to-native-sliding-sync/). Due to this development, I will be archiving this repo. If you still need it for any reason, please consider forking it. Happy matrixing 💙

# Matrix Sliding Sync helm chart

<a href="https://github.com/small-hack/matrix-sliding-sync-chart/releases"><img src="https://img.shields.io/github/v/release/small-hack/matrix-sliding-sync-chart?style=plastic&labelColor=blue&color=green&logo=GitHub&logoColor=white"></a>

This is a helm chart implementing [matrix-org/sliding-sync](https://github.com/matrix-org/sliding-sync/tree/main) for deployment on Kubernetes. It was originally designed for use as a subchart for [small-hack/matrix-chart](https://github.com/small-hack/matrix-chart), but it can be used stand alone as well.

See the [`README.md`](https://github.com/small-hack/matrix-sliding-sync-chart/blob/main/charts/matrix-sliding-sync/README.md) for docs auto-generated from the [`values.yaml`](https://github.com/small-hack/matrix-sliding-sync-chart/blob/main/charts/matrix-sliding-sync/values.yaml).

## TLDR

Read through the parameters and modify them locally before installing the chart:

```bash
# add the helm repo locally
helm repo add matrix-sliding-sync https://small-hack.github.io/matrix-sliding-sync-chart

# downloads the values.yaml locally
helm show values matrix-sliding-sync/matrix-sliding-sync > values.yaml

# install the chart
helm install my-release-name matrix-sliding-sync/matrix-sliding-sync --values values.yaml
```

Here's how I've been testing in the ci:

```bash
helm install matrix matrix/matrix --set postgresql.volumePermissions.enabled=false,postgresql.primary.networkPolicy.enabled=false,element.enabled=true,fullnameOverride=matrix-stack
helm install matrix-sliding-sync --set=postgresql.volumePermissions.enabled=false,postgresql.primary.networkPolicy.enabled=false,syncv3.server=http://matrix-stack-element matrix-sliding-sync/matrix-sliding-sync
```

## Status

Kinda working. Submit PRs or Issues if something specific isn't working
