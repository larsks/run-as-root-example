The `base` directory contains a simple Apache http Pod that will fail with:

```
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.130.0.54. Set the 'ServerName' directive globally to suppress this message
(13)Permission denied: AH00072: make_sock: could not bind to address [::]:80
(13)Permission denied: AH00072: make_sock: could not bind to address 0.0.0.0:80
no listening sockets available, shutting down
AH00015: Unable to open logs
```

The `run_as_root` directory contains a Kustomize overlay that adds the necessary configuration to permit the container to run as `root`, which allows Apache to bind to port 80 (and allows it to access the filesystems path in which it stores logs, pid files, etc).

## Deploying this example

These examples are meant to be deployed using [Kustomize](https://kustomize.io). You can view the final manifests by running:

```
kubectl kustomize run-as-root
```

You can deploy the example by running:

```
kubectl apply -k run-as-root
```

