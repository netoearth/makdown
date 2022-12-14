## The missing UI of Helm

![](https://miro.medium.com/max/700/1*nfrmjKIfO-iewPJTDDfOYw.png)

## What is Helm Dashboard

Helm-Dashboard offers a UI-driven way to view the installed `Helm` charts, see their revision history and corresponding k8s resources. Also, you can perform simple actions like roll back to a revision or upgrade to newer version. Helm dashboard is [Komodor](https://komodor.com/)'s second open source project after `ValidKube` .

![](https://miro.medium.com/max/700/0*gClBdWv0eBYiXuor.png)

Pic from [komodor](https://github.com/komodorio/helm-dashboard)

## Helm Dashboard Background

By the time `Helm` became a CNCF graduate project in April 2020, it was already in use by 70% of K8s users. One might even say that Helm opened the door to the global adoption of K8s, as it made it very easy to template, package, and deploy applications without needing a deep knowledge of K8s.

However, this also adds some challenges to operations and it becomes very difficult to do so at scale without really understanding the underlying Helm structure and information.

Due to the lack of a friendly user interface, `Helm` users forces to manually learn and execute commands through the CLI. In addition to being time-consuming, using the CLI makes it difficult to assess the impact of deploying or rolling back a `Helm` chart.

Comparing different versions of Helm Charts and their corresponding K8s resources is also a very inefficient process, especially when faced with troubleshooting issues in production.

Therefore Komodor decided to take the challenge and develop Helm Dashboard to make Helm operations more visual and easier.

## Helm Dashboard Core Features

Some of the core features of the tool are as follows:

-   View all installed Charts and their revision history
-   View list diffs for past revisions
-   Browse K8s resources generated by Chart
-   Easy to rollback or upgrade versions, with clear and simple manifest diffs
-   Integrate with popular tools
-   Easily switch between multiple clusters

## Helm Dashboard Install

Note, Helm v3.4.0+ is required for Helm dashboard.

To install Helm dashboard, you can simply run the following helm command:

```
$ helm plugin install https://github.com/komodorio/helm-dashboard.gitDownloading and installing helm-dashboard v0.2.3 ...https://github.com/komodorio/helm-dashboard/releases/download/v0.2.3/helm-dashboard_0.2.3_Linux_x86_64.tar.gzHelm Dashboard is installed, to start it, run in your terminal:    helm dashboardInstalled plugin: dashboard
```

To update the plugin to the latest version, run:

```
$ helm plugin update dashboard
```

To uninstall, run:

```
$ helm plugin uninstall dashboard
```

After install/upgrade Helm dashboard successfully, you can start the UI by typing:

```
$ helm dashboard$ helm dashboardINFO[0000] Helm Dashboard by Komodor, version 0.2.3 (549cdd9bfbdf32009f8dbbc240c59c86c2e430d7 @ 2022-10-26T14:27:14Z)...INFO[0000] Opening Web UI: http://0.0.0.0:8080
```

By default, the web server is only available locally. You can change that by specifying `HD_BIND` environment variable to the desired value. For example, `0.0.0.0` would bind to all IPv4 addresses or `[::0]` would be all IPv6 addresses.

If your port 8080 is busy, you can specify a different port to use via `--port <number>` command-line flag.

Now open a web browser, you should be able to access the dashboard:

![](https://miro.medium.com/max/700/1*DZYuynEyDGvTXcicLnscLw.png)

## Helm Dashboard Scanner Integrations

Upon startup, Helm Dashboard detects the presence of [Trivy](https://github.com/aquasecurity/trivy) and [Checkov](https://github.com/bridgecrewio/checkov) scanners. When available, these scanners are offered on k8s resources page, as well as install/upgrade preview page.

You can request scanning of the specific k8s resource in your cluster:

![](https://miro.medium.com/max/700/0*KJIeloT9AVcPcFqG.png)

Pic from [kumodor](https://github.com/komodorio/helm-dashboard)

If you want to validate the k8s manifest prior to installing/reconfiguring a Helm chart, look for ???Scan for Problems??? button at the bottom of the dialog:

![](https://miro.medium.com/max/700/0*JrPe3W4_NVFfEjbs.png)

Pic from [kumodor](https://github.com/komodorio/helm-dashboard)