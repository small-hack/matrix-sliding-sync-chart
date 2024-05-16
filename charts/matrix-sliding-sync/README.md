# matrix-sliding-sync

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v0.99.17](https://img.shields.io/badge/AppVersion-v0.99.17-informational?style=flat-square)

A Helm chart for Kubernetes

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | postgresql | 15.1.4 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| externalDatabase.database | string | `"matrix"` | name of the database to try and connect to |
| externalDatabase.enabled | bool | `false` | enable using an external database *instead of* the Bitnami PostgreSQL sub-chart if externalDatabase.enabled is set to true, postgresql.enabled must be set to false |
| externalDatabase.existingSecret | string | `""` | Name of existing secret to use for PostgreSQL credentials |
| externalDatabase.hostname | string | `""` | hostname of db server. Can be left blank if using postgres subchart |
| externalDatabase.password | string | `"changeme"` | password of matrix postgres user - ignored using exsitingSecret |
| externalDatabase.port | int | `5432` | which port to use to connect to your database server |
| externalDatabase.secretKeys.adminPasswordKey | string | `"postgresPassword"` | key in existingSecret with the admin postgresql password |
| externalDatabase.secretKeys.database | string | `"database"` | key in existingSecret with name of the database |
| externalDatabase.secretKeys.databaseHostname | string | `"hostname"` | key in existingSecret with hostname of the database |
| externalDatabase.secretKeys.databaseUsername | string | `"username"` | key in existingSecret with username for matrix to connect to db |
| externalDatabase.secretKeys.userPasswordKey | string | `"password"` | key in existingSecret with password for matrix to connect to db |
| externalDatabase.sslcert | string | `""` | optional: tls/ssl cert for postgresql connections |
| externalDatabase.sslkey | string | `""` | optional: tls/ssl key for postgresql connections |
| externalDatabase.sslmode | string | `""` | sslmode to use, example: verify-full |
| externalDatabase.sslrootcert | string | `""` | optional: tls/ssl root cert for postgresql connections |
| externalDatabase.username | string | `"matrix"` | username of matrix postgres user |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/matrix-org/sliding-sync"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.httpGet.path | string | `"/"` |  |
| livenessProbe.httpGet.port | string | `"http"` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| postgresql.enabled | bool | `true` | Whether to deploy the Bitnami Postgresql sub chart If postgresql.enabled is set to true, externalDatabase.enabled must be set to false else if externalDatabase.enabled is set to true, postgresql.enabled must be set to false |
| postgresql.global.postgresql.auth.existingSecret | string | `""` | Name of existing secret to use for PostgreSQL credentials |
| postgresql.global.postgresql.auth.password | string | `"changeme"` | password of matrix postgres user - ignored using exsitingSecret |
| postgresql.global.postgresql.auth.port | int | `5432` | which port to use to connect to your database server |
| postgresql.global.postgresql.auth.secretKeys.adminPasswordKey | string | `"postgresPassword"` | key in existingSecret with the admin postgresql password |
| postgresql.global.postgresql.auth.secretKeys.database | string | `"database"` | key in existingSecret with name of the database |
| postgresql.global.postgresql.auth.secretKeys.databaseHostname | string | `"hostname"` | key in existingSecret with hostname of the database |
| postgresql.global.postgresql.auth.secretKeys.databaseUsername | string | `"username"` | key in existingSecret with username for matrix to connect to db |
| postgresql.global.postgresql.auth.secretKeys.userPasswordKey | string | `"password"` | key in existingSecret with password for matrix to connect to db |
| postgresql.global.postgresql.auth.username | string | `"matrix-sliding-sync"` | username of matrix postgres user |
| postgresql.primary.initdb | object | `{"scriptsConfigMap":"{{ .Release.Name }}-postgresql-initdb"}` | run the scripts in templates/postgresql/initdb-configmap.yaml If using an external Postgres server, make sure to configure the database ref: https://github.com/matrix-org/synapse/blob/master/docs/postgres.md |
| postgresql.primary.persistence | object | `{"enabled":false,"size":"8Gi"}` | persistent volume claim configuration for postgresql to persist data |
| postgresql.primary.persistence.enabled | bool | `false` | Enable PostgreSQL Primary data persistence using PVC |
| postgresql.primary.persistence.size | string | `"8Gi"` | size of postgresql volume claim |
| postgresql.primary.podSecurityContext.enabled | bool | `true` |  |
| postgresql.primary.podSecurityContext.fsGroup | int | `1000` |  |
| postgresql.primary.podSecurityContext.runAsUser | int | `1000` |  |
| postgresql.volumePermissions.enabled | bool | `true` | Enable init container that changes the owner and group of the PVC |
| readinessProbe.httpGet.path | string | `"/"` |  |
| readinessProbe.httpGet.port | string | `"http"` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automount | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| syncv3.bindaddr | string | `"0.0.0.0:8008"` | SYNCV3_BINDADDR - The interface and port to listen on. (Supports unix socket: /path/to/socket) |
| syncv3.db | string | `""` | SYNCV3_DB - Required. The postgres connection string: https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING |
| syncv3.log_level | string | `"info"` | SYNCV3_LOG_LEVEL - The level of verbosity for messages logged. Available values are trace, debug, info, warn, error and fatal |
| syncv3.max_db_conn | string | `""` | SYNCV3_MAX_DB_CONN - Default: unset. Max database connections to use when communicating with postgres. Unset or 0 means no limit. |
| syncv3.otlp_password | string | `""` | SYNCV3_OTLP_PASSWORD - Default: unset. The OTLP password for Basic auth. If unset, does not send an Authorization header. |
| syncv3.otlp_url | string | `""` | SYNCV3_OTLP_URL - Default: unset. The OTLP HTTP URL to send spans to e.g https://localhost:4318 - if unset does not send OTLP traces. |
| syncv3.otlp_username | string | `""` | SYNCV3_OTLP_USERNAME - Default: unset. The OTLP username for Basic auth. If unset, does not send an Authorization header. |
| syncv3.pprof | string | `""` | SYNCV3_PPROF - Default: unset. The bind addr for pprof debugging e.g ':6060'. If not set, does not listen. |
| syncv3.prom | string | `""` | SYNCV3_PROM - Default: unset. The bind addr for Prometheus metrics, which will be accessible at /metrics at this address. |
| syncv3.secret | string | `""` | SYNCV3_SECRET - Required. A secret to use to encrypt access tokens. Must remain the same for the lifetime of the database. |
| syncv3.sentry_dsn | string | `""` | SYNCV3_SENTRY_DSN - Default: unset. The Sentry DSN to report events to e.g https://sliding-sync@sentry.example.com/123 - if unset does not send sentry events. |
| syncv3.server | string | `""` | SYNCV3_SERVER - Required. The destination homeserver to talk to (CS API HTTPS URL) e.g 'https://matrix-client.matrix.org' (Supports unix socket: /path/to/socket) |
| syncv3.tlsCert | string | `""` | SYNCV3_TLS_CERT - Default: unset. Path to a certificate file to serve to HTTPS clients. Specifying this enables TLS on the bound address. |
| syncv3.tlsKey | string | `""` | SYNCV3_TLS_KEY - Default: unset. Path to a key file for the certificate. Must be provided along with the certificate file. |
| tolerations | list | `[]` |  |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.13.1](https://github.com/norwoodj/helm-docs/releases/v1.13.1)
