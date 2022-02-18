---
date: 2019-12-12T00:00:00-00:00
title: "Upgrading"
linkTitle: "Upgrading"
weight: 12
description: How to upgrade the Anka Build Cloud
---

### Before you begin

{{< hint info >}}
We follow [semantic versioning](https://semver.org/); minor and major version increases can have significant changes and should be carefully considered.
{{< /hint >}}

{{< hint info >}}
Before upgrading, check if your current version is noted in the [Pre-Upgrade Considerations]({{< relref "arm/Anka Build Cloud/upgrading.md#pre-upgrade-considerations" >}}) and adjust your upgrade plan accordingly.
{{< /hint >}}

{{< hint info >}}
The Controller and Anka Nodes communicate through an agent running separate from from the Anka Virtualization/CLI tool, but on the same machine. When you upgrade the Controller, the node agent notices that the agent and controller versions differ and will create a task for each Node. This task will trigger the agent to perform a self-update and restart. While most situations this is seamless, we recommend checking the agent version post-upgrade on each Node with `ankacluster --version` to ensure it was upgraded properly. Nodes must be joined to the controller to receive the task to upgrade.

If necessary, you can [force the proper agent version task creation through the Controller API.]({{< relref "arm/Anka Build Cloud/working-with-controller-and-API.md#force-node-agent-update" >}}). Alternatively you can also disjoin the Nodes first, do the upgrade of the Controller, and then manually execute `curl -O http://**{controllerUrlHere}**/pkg/AnkaAgent.pkg && sudo installer -pkg AnkaAgent.pkg -tgt /` on each node individually.
{{< /hint >}}

{{< hint info >}}
It is generally safe to upgrade the controller while VMs are running and nodes are joined. However, if you can, we do recommend temporarily pausing CI/CD jobs or assigning to agents and letting the currently running jobs drain before moving forward.
{{< /hint >}}

{{< hint info >}}
- We recommend [snapshotting your etcd database](https://etcd.io/docs/v3.5/op-guide/recovery/#snapshotting-the-keyspace) regularly, but especially before an upgrade.
{{< /hint >}}

{{< hint info >}}
- The following steps also apply to downgrading, though, you need to forcefully downgrade the cluster agent on each of your nodes.
{{< /hint >}}

{{< hint warning >}}
If you are upgrading the host/node macOS version, please disjoin and join the node to the controller using the `ankacluster` command.
{{< /hint >}}
### Pre-upgrade Considerations

| Existing Version | Target Version | Recommendation |
| --- | --- | --- |
| 1.18.0 | > 1.18.0 | Please note that there is a temporary workaround required for a bug that started in versions after 1.18.0 of the Controller/Registry agent which runs on your nodes. All versions of the agent, when noticing that the version of itself does not match the version of the controller, will perform a self-upgrade and restart. The restart seems to be problematic on some setups and leaves a zombie anka_agent process and and Offline status in the controller UI. To work around the bug when upgrading your controller/registry, you'll need to change the existing steps to include: <ul><li>Disjoining all of the nodes first</li><li>Do the controller/registry upgrade</li><li>Run `curl -O http://**{controllerUrlHere}**/pkg/AnkaAgent.pkg && sudo installer -pkg AnkaAgent.pkg -tgt /` on each node to download the new version</li><li>And finally join each node back</li></ul>We will be fixing the bug soon. Thanks for your understanding and we are sorry for the inconvenience this causes.
| x.xx.x | 1.20.0 | _Minimum Registry version required for Controller - 1.19.0_

### Upgrade Procedure

#### Docker

  1. Make a backup of your `docker-compose.yml`.
  2. [Download and extract the latest package]({{< relref "arm/Anka Build Cloud/setup-on-linux-with-docker.md#step-2-install-the-anka-build-cloud-controller--registry" >}}).
  3. Configure the values in the `docker-compose.yml` or copy your previous `docker-compose.yml` to the new directory.
  4. Run `docker-compose build` to prepare the new docker tag.
  5. Run `docker-compose down` to take down the older version.
  6. Run `docker-compose up -d` in the newer version directory.

#### Native macOS package

  1. Make a backup of your `/usr/local/bin/anka-controllerd`.
  2. Install the new .pkg (see the [MacOS Guide]({{< relref "arm/Anka Build Cloud/setup-on-macos.md" >}})).
  3. Run `sudo anka-controller restart`.