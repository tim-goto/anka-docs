---
---

#### Resource Permissions

{{< hint warning >}}
Node Groups are disabled while Resource Management is enabled.
{{< /hint >}}

The Resource Permissions feature is enabled by setting **ANKA_ENABLE_RESOURCE_MANAGEMENT** to **true** in your configuration. Once enabled, it unlocks the Resources tab under **/permission-groups**.

Within Resources you will be able to, depending on the Component selected, add specific Nodes or Templates to the Group. This limits the Group to certain actions that can be performed against the Resource. An example of this is allowing the iOS team/group to distribute specific Templates to specific Nodes, but not create VM Instances or delete the Node.

{{< imgwithlink src="images/anka-build-cloud/advanced-security-features/resources-basic.png" >}}

In the [previous section on Permissions](#permission-groups), we joined a Node using a credential with the Permission Group of `node` attached. This Group only has Permissions to perform the minimum required actions to run as an Anka Node and communicate with the Controller. We *did not* add Resources to it though (even though we technically could) so we can instead have team specific Groups. This is the first recommendation method of grouping permissions: Each team gets only Resources assigned to their Group, and other Groups handle the ability to request certain information from and perform actions to the Controller and Registry.

{{< hint warning >}}
**It's important to understand that a single credential, like a [UAK]({{< relref "anka-build-cloud/Advanced Security Features/uak-tap-authentication.md" >}}) or a [Certificate]({{< relref "anka-build-cloud/Advanced Security Features/certificate-authentication.md" >}}), should only ever be used by a specific user and client.** You wouldn't ever want to share the Node credential with a team for example. Create a second credential for that team, then in order for the Node to be able to access the team's credential, add the team's Group to the Node credential.
{{< /hint >}}

1. Create two groups: `ios` and `instance-control`.

2. Under the `ios` Group > Resources, add the Template Resource you want this team to access. The bare minimum permissions are seen in the image below.

{{< imgwithlink src="images/anka-build-cloud/advanced-security-features/perm-groups-ios-resources-template.png" >}}

2. Under the `instance-control` Group > Permissions, add all of the Instances Permissions like in the image below.

{{< imgwithlink src="images/anka-build-cloud/advanced-security-features/perm-groups-instance-control-perms.png" >}}

2. Now create a *new credential* (not Group) named `service-user` and attach those two groups. We'll use [UAKs]({{< relref "anka-build-cloud/Advanced Security Features/uak-tap-authentication.md" >}}) for this example. There is no need for the `service-user` to have its own group as it will get the VM start and terminate permissions from `instance-control` group and Template/Node permissions from the `ios` group.

3. Attach the group `ios` to the `node` credential we created in the previous section and joined our node with so that that it can also collect information about the Template in order to start the VM Instance properly (it checks the download size of the template before pulling). Your UAK setup should look something like this image.

{{< imgwithlink src="images/anka-build-cloud/advanced-security-features/perm-groups-uak-service-user-list.png" >}}

We can now use `service-user` in our CI/CD tools to communicate with the Controller when an `ios` team member triggers a job and that job requests a VM Instance to run the job commands inside of. When the `service-user` makes an API call to start a VM Instance, it will pass in the `ios` group, as that group has access to the template being targeted.

##### Answers to Frequently Asked Questions

- The Nodes joined to the Controller must have Permissions to access the Template being used to start a VM.
- Node Groups differ from Permissions Groups and are disabled when this feature is enabled.
- Save Image requests can only target Instances that belong to a group the user has access to.