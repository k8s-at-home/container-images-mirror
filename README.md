# Container Images Mirror

Images are hosted on Github Container Registry [here](https://github.com/orgs/k8s-at-home/packages?ecosystem=container&visibility=public).

## Purpose

This is to get around Docker Hub rate-limiting (100 pulls / 6 hours, or authenticated 200 pulls / 6 hours). It is considered a stop-gap until the maintainers of the applications below support a different Container Registry.

## Supported images

When upstream maintainers add support for an additional registry, the images here will be purged after awhile.

| Name                                                                                            | Upstream Issue                                                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [code-server](https://github.com/cdr/code-server)                                               | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/cdr/code-server/3335)](https://github.com/cdr/code-server/issues/3335)                                                   |
| [chrony](https://github.com/mlichvar/chrony)                                               |                                                    |
| [frigate](https://github.com/blakeblackshear/frigate)                                           | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/blakeblackshear/frigate/1490)](https://github.com/blakeblackshear/frigate/issues/1490)                                   |
| [jellyfin](https://github.com/jellyfin/jellyfin)                                                | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/jellyfin/jellyfin/6024)](https://github.com/jellyfin/jellyfin/issues/6024)                                               |
| [node-red](https://github.com/node-red/node-red)                                                | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/node-red/node-red/3107)](https://github.com/node-red/node-red/issues/3107)                                               |
| [prometheus-qbittorrent-exporter](https://github.com/esanchezm/prometheus-qbittorrent-exporter) | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/esanchezm/prometheus-qbittorrent-exporter/12)](https://github.com/esanchezm/prometheus-qbittorrent-exporter/issues/12)   |
| [traefik](https://github.com/traefik/traefik)                                                   | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/traefik/traefik/8149)](https://github.com/traefik/traefik/issues/8149)                                                   |
| [unpoller](https://github.com/unpoller/unpoller)                                                | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/unpoller/unpoller/368)](https://github.com/unpoller/unpoller/issues/368)                                                 |
| [grafana](https://github.com/grafana/grafana)                                                   | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/grafana/grafana/27677)](https://github.com/grafana/grafana/issues/27677)                                                 |
| [loki](https://github.com/grafana/loki)                                                         | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/grafana/loki/4143)](https://github.com/grafana/loki/issues/4143)                                                         |
| [reloader](https://github.com/stakater/Reloader)                                                | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/stakater/Reloader/255)](https://github.com/stakater/Reloader/issues/255)                                                 |
| [eclipse-mosquitto](https://github.com/eclipse/mosquitto)                                       | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/eclipse/mosquitto/2279)](https://github.com/eclipse/mosquitto/issues/2279)                                               |
| [velero](https://github.com/vmware-tanzu/velero)                                                | [![GitHub issue status](https://img.shields.io/github/issues/detail/state/vmware-tanzu/velero/4106)](https://github.com/vmware-tanzu/velero/issues/2279)                                           |

## Contributing

You can discover containers running in your cluster from Docker Hub by using the following command:

```
kubectl get pods --all-namespaces -o=jsonpath="{range .items[*]}{'\n'}{range .spec.containers[*]}{.image}{'\n'}{end}{end}" | sort | uniq | grep -Ev 'quay|gcr|ghcr|ecr' |  sed -e 's/docker\.io\///g' | sort | uniq
```

After you have determined some image you want to mirror, do the following:

- If not already created, create an issue upstream asking for them to support an additional registry.
- Open a PR adding a new application to the `apps` folder, update the `README.md` with the issue link, and then update `.github/renovate.json5` to auto merge it.
- Remind us to make the image public after the PR is merged ;)
