# wallboard-helm-chart

helm install my-release wallboard-0.1.0.tgz --set daemonset.optionalVolume.enabled=true --set daemonset.optionalVolume.hostPath=/home/hash/wallpaper.jpg

--set daemonset.url=https://your-new-url.com