# zuzak/grafana

Grafana dashboard JSON files for the homelab cluster. Grafana pulls from this
repo every 60 seconds via Git sync, so a merge to main is live within a minute.

## Layout

| Path | Contents |
|---|---|
| `kubernetes/` | Node and cluster metrics |
| `storage/` | Persistent storage (Longhorn, CloudNativePG) |
| `services/` | Per-service dashboards |

## Attribution and licensing

Community dashboards are reproduced here with modifications (plain-English
panel descriptions; datasource UID corrections for this cluster's Prometheus
and Loki instances).

| File | Source | Author | License |
|---|---|---|---|
| `kubernetes/node-exporter-full.json` | [grafana.com/dashboards/1860](https://grafana.com/grafana/dashboards/1860) · [rfmoz/grafana-dashboards](https://github.com/rfmoz/grafana-dashboards) | rfmoz | Apache-2.0 |
| `kubernetes/kubernetes-pods.json` | [grafana.com/dashboards/15760](https://grafana.com/grafana/dashboards/15760) · [dotdc/grafana-dashboards-kubernetes](https://github.com/dotdc/grafana-dashboards-kubernetes) | dotdc | Apache-2.0 |
| `storage/longhorn.json` | [grafana.com/dashboards/13032](https://grafana.com/grafana/dashboards/13032) · [longhorn/longhorn](https://github.com/longhorn/longhorn) | phanle1010 | Apache-2.0 |
| `storage/cnpg.json` | [grafana.com/dashboards/20417](https://grafana.com/grafana/dashboards/20417) · [cloudnative-pg/cloudnative-pg](https://github.com/cloudnative-pg/cloudnative-pg) | CloudNativePG | Apache-2.0 |
| `services/argocd.json` | [grafana.com/dashboards/19993](https://grafana.com/grafana/dashboards/19993) · [adinhodovic/argo-cd-mixin](https://github.com/adinhodovic/argo-cd-mixin) | adinhodovic | no license declared |
| `services/authentik.json` | [goauthentik/authentik · website/static/monitoring/](https://github.com/goauthentik/authentik/blob/main/website/static/monitoring/grafana-dashboard.json) | Jens Langhammer | CC BY-SA 4.0 |
| `services/nginx-ingress.json` | [grafana.com/dashboards/9614](https://grafana.com/grafana/dashboards/9614) · [kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx) | gonzalesraul | Apache-2.0 |
| `services/loki.json` | [grafana.com/dashboards/13639](https://grafana.com/grafana/dashboards/13639) | sadlil | no license declared |
| `services/grocy.json` | this repo | zuzak / claude-zuzak | — |
| `claude-code-telemetry.json` | this repo | zuzak / claude-zuzak | — |

## Datasource UIDs

| Datasource | UID |
|---|---|
| Prometheus | `prometheus` |
| Loki | `loki` |
| Lifestyle Prometheus | `lifestyle-prometheus` |

Community dashboards often hardcode author-specific UIDs. Fix before committing.
