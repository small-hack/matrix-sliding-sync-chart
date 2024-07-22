# matrix-sliding-sync

![Version: 0.5.8](https://img.shields.io/badge/Version-0.5.8-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v0.99.19](https://img.shields.io/badge/AppVersion-v0.99.19-informational?style=flat-square)

A Helm chart for deploying matrix sliding sync on Kubernetes

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| jessebot |  | <https://github.com/jessebot> |

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | postgresql | 15.5.17 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| existingEnvSecret | string | `""` | existing kubernetes secret for ALL syncv3 env vars listed below. if set, ignores all values under syncv3 including syncv3.db and syncv3.otlp. |
| externalDatabase.database | string | `"syncv3"` | name of the database to try and connect to |
| externalDatabase.enabled | bool | `false` | enable using an external database *instead of* the Bitnami PostgreSQL sub-chart if externalDatabase.enabled is set to true, postgresql.enabled must be set to false |
| externalDatabase.hostname | string | `""` | hostname of db server. Can be left blank if using postgres subchart |
| externalDatabase.password | string | `"changeme"` | password of matrix-sliding-sync postgres user - ignored using exsitingSecret |
| externalDatabase.port | int | `5432` | which port to use to connect to your database server |
| externalDatabase.sslcert | string | `""` | optional: tls/ssl cert for postgresql connections |
| externalDatabase.sslkey | string | `""` | optional: tls/ssl key for postgresql connections |
| externalDatabase.sslmode | string | `""` | sslmode to use, example: verify-full |
| externalDatabase.sslrootcert | string | `""` | optional: tls/ssl root cert for postgresql connections |
| externalDatabase.username | string | `"syncv3"` | username of matrix-sliding-sync postgres user |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy. if image.tag is set to "latest", set to "Always" |
| image.repository | string | `"ghcr.io/matrix-org/sliding-sync"` |  |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.enabled | bool | `false` | enable a liveness probe on the deployment |
| livenessProbe.httpGet.path | string | `"/"` |  |
| livenessProbe.httpGet.port | string | `"http"` |  |
| nameOverride | string | `""` |  |
| networkPolicies.enabled | bool | `true` | whether to enable kubernetes network policies or not |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| postgresql.enabled | bool | `true` | Whether to deploy the Bitnami Postgresql sub chart If postgresql.enabled is set to true, externalDatabase.enabled must be set to false else if externalDatabase.enabled is set to true, postgresql.enabled must be set to false |
| postgresql.global.postgresql.auth.database | string | `"syncv3"` | name of the database |
| postgresql.global.postgresql.auth.existingSecret | string | `""` | Name of existing secret to use for PostgreSQL credentials |
| postgresql.global.postgresql.auth.password | string | `"changeme"` | password of matrix-sliding-sync postgres user - ignored using exsitingSecret |
| postgresql.global.postgresql.auth.port | int | `5432` | which port to use to connect to your database server |
| postgresql.global.postgresql.auth.secretKeys.adminPasswordKey | string | `"postgresPassword"` | key in existingSecret with the admin postgresql password |
| postgresql.global.postgresql.auth.secretKeys.database | string | `"database"` | key in existingSecret with name of the database |
| postgresql.global.postgresql.auth.secretKeys.databaseHostname | string | `"hostname"` | key in existingSecret with hostname of the database |
| postgresql.global.postgresql.auth.secretKeys.databaseUsername | string | `"username"` | key in existingSecret with username for matrix-sliding-sync to connect to db |
| postgresql.global.postgresql.auth.secretKeys.userPasswordKey | string | `"password"` | key in existingSecret with password for matrix-sliding-sync to connect to db |
| postgresql.global.postgresql.auth.username | string | `"syncv3"` | username of matrix-sliding-sync postgres user |
| postgresql.primary.initdb | object | `{"scripts":{"matrix_sliding_sync.sql":"CREATE DATABASE matrix ENCODING 'UTF8' LOCALE 'C' TEMPLATE template0 OWNER syncv3;\nGRANT ALL PRIVILEGES ON DATABASE matrix-sliding-sync TO syncv3;\nGRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO syncv3;\n"}}` | If using an external Postgres server, make sure to configure the database ref: https://github.com/matrix-org/synapse/blob/master/docs/postgres.md |
| postgresql.primary.initdb.scripts | object | `{"matrix_sliding_sync.sql":"CREATE DATABASE matrix ENCODING 'UTF8' LOCALE 'C' TEMPLATE template0 OWNER syncv3;\nGRANT ALL PRIVILEGES ON DATABASE matrix-sliding-sync TO syncv3;\nGRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO syncv3;\n"}` | Map of initdb scripts. Specify dictionary of scripts to be run at first boot |
| postgresql.primary.initdb.scripts."matrix_sliding_sync.sql" | string | `"CREATE DATABASE matrix ENCODING 'UTF8' LOCALE 'C' TEMPLATE template0 OWNER syncv3;\nGRANT ALL PRIVILEGES ON DATABASE matrix-sliding-sync TO syncv3;\nGRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO syncv3;\n"` | note, if you change postgresql.global.postgresql.auth.username, or postgresql.global.postgresql.auth.secretKeys.userPasswordKey, please also change it in the 3 lines of this script |
| postgresql.primary.podSecurityContext.enabled | bool | `true` |  |
| postgresql.primary.podSecurityContext.fsGroup | int | `1000` |  |
| postgresql.primary.podSecurityContext.runAsUser | int | `1000` |  |
| postgresql.tls.autoGenerated | bool | `false` | Generate automatically self-signed TLS certificates |
| postgresql.tls.certCAFilename | string | `""` | CA Certificate filename |
| postgresql.tls.certFilename | string | `""` | Certificate filename |
| postgresql.tls.certKeyFilename | string | `""` | Certificate key filename |
| postgresql.tls.certificatesSecret | string | `""` | Name of an existing secret that contains the certificates |
| postgresql.tls.crlFilename | string | `""` | File containing a Certificate Revocation List |
| postgresql.tls.enabled | bool | `false` | Enable TLS traffic support for postgresql, see [bitnami/charts/postgresql#securing-traffic-using-tls](https://github.com/bitnami/charts/tree/main/bitnami/postgresql#securing-traffic-using-tls) |
| postgresql.tls.preferServerCiphers | bool | `true` | Whether to use the server's TLS cipher preferences rather than the client's |
| postgresql.volumePermissions.enabled | bool | `true` | Enable init container that changes the owner and group of the PVC |
| readinessProbe.enabled | bool | `false` | enable a readiness probe on the deployment |
| readinessProbe.httpGet.path | string | `"/"` |  |
| readinessProbe.httpGet.port | string | `"http"` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.annotations | object | `{}` | annotations for your service |
| service.port | int | `80` | Port of service |
| service.targetPort | int | `8008` | targetPort of service. should be the same as port for syncv3.bindaddr |
| service.type | string | `"ClusterIP"` | type of service |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| syncv3.bindaddr | string | `"0.0.0.0:8008"` | SYNCV3_BINDADDR - The interface and port to listen on. (Supports unix socket: /path/to/socket) |
| syncv3.db | string | `""` | SYNCV3_DB - db connection string: https://www.postgresql.org/docs/current/libpq-connect.html if db is empty, you must either provide postgresql or externalDatabase parameters, OR set syncv3.existingDbSecret and syncv3.dbSecretKey |
| syncv3.dbSecretKey | string | `"SYNCV3_DB"` | db key in existing Db Secret for |
| syncv3.existingDbSecret | string | `""` | use an existing kubernetes secret for the db connection connection string. if set, ignores syncv3.db |
| syncv3.existingSyncv3Secret | string | `""` | if set, we'll grab your SYNCV3_SECRET from an existing kubernetes secret and ignore syncv3.secret |
| syncv3.logLevel | string | `"info"` | SYNCV3_LOG_LEVEL - The level of verbosity for messages logged. Available values are trace, debug, info, warn, error and fatal |
| syncv3.maxDbConn | string | `""` | SYNCV3_MAX_DB_CONN - Default: unset. Max database connections to use when communicating with postgres. Unset or 0 means no limit. |
| syncv3.otlp.existingSecret | string | `nil` |  |
| syncv3.otlp.password | string | `""` | SYNCV3_OTLP_PASSWORD - Default: unset. The OTLP password for Basic auth. If unset, does not send an Authorization header. |
| syncv3.otlp.url | string | `""` | SYNCV3_OTLP_URL - Default: unset. The OTLP HTTP URL to send spans to e.g https://localhost:4318 - if unset does not send OTLP traces. |
| syncv3.otlp.username | string | `""` | SYNCV3_OTLP_USERNAME - Default: unset. The OTLP username for Basic auth. If unset, does not send an Authorization header. |
| syncv3.pprof | string | `""` | SYNCV3_PPROF - Default: unset. The bind addr for pprof debugging e.g ':6060'. If not set, does not listen. |
| syncv3.prom | string | `""` | SYNCV3_PROM - Default: unset. The bind addr for Prometheus metrics, which will be accessible at /metrics at this address. |
| syncv3.secret | string | `""` | SYNCV3_SECRET - Required. A secret to use to encrypt access tokens. Must remain the same for the lifetime of the database. If both syncv3.secret and syncv3.existingSecret are not set, we will autogenerate this value |
| syncv3.sentryDsn | string | `""` | SYNCV3_SENTRY_DSN - Default: unset. The Sentry DSN to report events to e.g https://sliding-sync@sentry.example.com/123 - if unset does not send sentry events. |
| syncv3.server | string | `""` | SYNCV3_SERVER - Required. The destination homeserver to talk to (CS API HTTPS URL) e.g 'https://matrix-client.matrix.org' (Supports unix socket: /path/to/socket) |
| syncv3.syncv3SecretKey | string | `"SYNCV3_SECRET"` | secret key to get synvcv3 secret from in existing kubernetes secret. |
| syncv3.tlsCert | string | `""` | SYNCV3_TLS_CERT - Default: unset. Path to a certificate file to serve to HTTPS clients. Specifying this enables TLS on the bound address. |
| syncv3.tlsKey | string | `""` | SYNCV3_TLS_KEY - Default: unset. Path to a key file for the certificate. Must be provided along with the certificate file. |
| tolerations | list | `[]` |  |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.13.1](https://github.com/norwoodj/helm-docs/releases/v1.13.1)
