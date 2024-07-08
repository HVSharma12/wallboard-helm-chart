# Wallboard Helm Chart

This Helm chart is used to deploy the Wallboard application as a DaemonSet on a Kubernetes cluster. It includes options to customize the deployment, such as changing the wallpaper and disabling the VNC service.

## Prerequisites

- Kubernetes cluster
- Helm installed and configured

## Installing the Chart

### Default Installation

To install the chart with the release name `wallboard`:

```bash
helm install wallboard ./wallboard-chart
```

### Customizing the Deployment

#### To change the wallpaper:

```bash
helm install wallboard ./wallboard-chart \
  --set daemonset.optionalVolume.enabled=true \
  --set daemonset.optionalVolume.hostPath=/path/to/your/wallpaper.jpg \
```

#### To disable VNC:

```bash
helm install wallboard ./wallboard-chart \
  --set vnc.enabled=false
```


## Uninstalling the Chart

To uninstall/delete the `wallboard` deployment:

```bash
helm uninstall wallboard
```

## Configuration

The following table lists the configurable parameters of the Wallboard chart and their default values.

| Parameter                              | Description                                             | Default                                          |
|----------------------------------------|---------------------------------------------------------|--------------------------------------------------|
| `namespace`                            | Namespace for the deployment                            | `wallboard`                                      |
| `vnc.enabled`                          | Enable/disable the VNC container                        | `true`                                           |
| `daemonset.name`                       | Name of the DaemonSet                                   | `wallboard`                                      |
| `daemonset.labels.name`                | Label name for the DaemonSet                            | `test-wallboard`                                 |
| `daemonset.url`                        | URL for the wallboard application                       | `https://google.com`                             |
| `daemonset.images.x11`                 | Image for the X11 init container                        | `registry.opensuse.org/home/atgracey/wallboardos/15.5/x11:notaskbar` |
| `daemonset.images.audio`               | Image for the audio init container                      | `registry.opensuse.org/home/atgracey/wallboardos/15.5/pa:latest`       |
| `daemonset.images.wallboard`           | Image for the wallboard container                       | `docker.io/atgracey/kiosk-test:latest`           |
| `daemonset.images.vnc`                 | Image for the VNC container                             | `registry.opensuse.org/home/atgracey/wallboardos/15.5/vnc:vnc`        |
| `daemonset.imagePullPolicy`            | Image pull policy                                       | `Always`                                         |
| `daemonset.runAsUser`                  | User ID to run the wallboard container                  | `1000`                                           |
| `daemonset.optionalVolume.enabled`     | Enable/disable the optional volume for wallpaper        | `false`                                          |
| `daemonset.optionalVolume.hostPath`    | Host path for the optional volume                       | `""`                                             |
| `daemonset.optionalVolume.mountPath`   | Mount path inside the container for the optional volume | `/usr/share/wallpapers/openSUSEdefault/contents/images/1920x1080.jpg` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
helm install wallboard ./wallboard-chart --set daemonset.runAsUser=1001
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
helm install wallboard ./wallboard-chart -f values.yaml
```

