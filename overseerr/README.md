# Overseerr

## Add repository

```
helm repo add k8s-at-home https://k8s-at-home.com/charts/
helm repo update
```

## Install chart

```
kubectl apply -f overseerr-config-pv.yaml
helm upgrade --install overseerr k8s-at-home/overseerr -f custom-values.yaml
```

## Default values

```
#
# IMPORTANT NOTE
#
# This chart inherits from our common library chart. You can check the default values/options here:
# https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml
#

image:
  # -- image repository
  repository: ghcr.io/sct/overseerr
  # -- image tag
  tag: 1.26.1
  # -- image pull policy
  pullPolicy: IfNotPresent

# -- environment variables.
# @default -- See below
env:
  # -- Set the container timezone
  TZ: UTC
  # -- Set the application log level
  LOG_LEVEL: info

# -- Configures service settings for the chart.
# @default -- See values.yaml
service:
  main:
    ports:
      http:
        port: 5055

ingress:
  # -- Enable and configure ingress settings for the chart under this key.
  # @default -- See values.yaml
  main:
    enabled: false

# -- Configure persistence settings for the chart under this key.
# @default -- See values.yaml
persistence:
  config:
    enabled: false
    mountPath: /app/config
```