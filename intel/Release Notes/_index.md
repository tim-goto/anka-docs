---
date: 2018-03-06
title: "Release Notes"
weight: 100
---

## Current Versions

### Anka Virtualization CLI 2.5.7 (2.5.7.148) - Aug 2nd, 2022

{{< hint warning >}}

##### Important considerations for this release

- Upgrading Addons from the previous patch version of anka is recommended but not fully required.


For more details, take a look at our [pre-upgrade considerations]({{< relref "intel/upgrading.md#pre-upgrade-considerations" >}}).
{{< /hint >}}

- **Bug Fix:** Inner VM reboots would cause black screens or panics.
- **Bug Fix:** License errors would not display in STDERR.
- **Improvement:** Security patches for VM networking.
<!-- - **New Feature (experimental):** [Ability to separate runtime image from static image storage directories]({{< relref "Whats New/anka-2.5.5/index.md#ability-to-separate-runtime-image-from-static-image-storage-directories-experimental" >}}) -->

---

## Previous Versions

### Anka Virtualization CLI 2.5.6 (2.5.6.147) - June 29th, 2022

{{< hint warning >}}

##### Important considerations for this release

- Upgrading Addons from the previous patch version of anka is recommended but not fully required.


For more details, take a look at our [pre-upgrade considerations]({{< relref "intel/upgrading.md#pre-upgrade-considerations" >}}).
{{< /hint >}}

- **Bug Fix:** `anka registry pull` would under certain conditions throw `ZeroDivisionError: float division by zero`.
- **Bug Fix:** `anka run` was not sourcing the shell profile files and interpolating variables. (requires addons upgrade)
- **Bug Fix:** Duplicate vnc_port field in the `anka --machine-readable show` output.
- **Bug Fix:** Inability to use .app installers with `anka create` when they're stored in /tmp.
- **Improvement:** Support for Ventura (13.0).
- **Improvement:** Port forwarding rewrite allowing for more network/communication stability.

### Anka Virtualization CLI 2.5.5 (2.5.5.143) - April 19th, 2022

{{< hint warning >}}

##### Important considerations for this release

- This is a patch for the existing 2.5.5.142 release.
- Upgrading Addons from the previous minor version of anka is recommended but not required.


For more details, take a look at our [pre-upgrade considerations]({{< relref "intel/upgrading.md#pre-upgrade-considerations" >}}).
{{< /hint >}}

- **Bug Fix:** Continued: `anka run` hangs when executing a command.
- **Improvement:** `anka registry --machine-readable check-download-size` now returns a boolean instead of "yes" or "no".

### Anka Virtualization CLI 2.5.5 (2.5.5.142) - April 11th, 2022

{{< hint warning >}}

##### Important considerations for this release

- Upgrading Addons from the previous minor version of anka is recommended but not required.


For more details, take a look at our [pre-upgrade considerations]({{< relref "intel/upgrading.md#pre-upgrade-considerations" >}}).
{{< /hint >}}

- **Bug Fix:** `anka cp` and `anka run` hang when executing + `ankactl: communication error: Operation timed out` errors after resuming VMs (addons upgrade required).
- **Bug Fix:** When two pulls are happening on the same machine for the same template and tag, it can sometimes cause a failure with `anka: no such version`.
- **Bug Fix:** Rarely `anka registry pull` would become stuck.
- **Bug Fix:** When the machine's disk was full, `anka registry pull` would report 100%/successfully pulled.
- **Bug Fix:** The Anka uninstaller was deleting the controller package installed on the same machine.
- **Bug Fix:** `anka registry pull` speed limitations fixed/removed.
- **Bug Fix:** `anka registry pull` can fail with `could not create disk image, status 74.` and then subsequent pulls immediately show 100%. This results in a broken VM.
- **Bug Fix:** Network/IP detection can very rarely choose the wrong IP on 11.6.4 VMs.
- **Bug Fix:** `block_nocache` was not working properly.
- **Improvement:** Network isolation now support bridged networking VMs (`anka modify VMNAME set network-card --no-local`).
- **Improvement:** Monterey VM performance.
- **New Feature:** [`anka show` now displays cpu usage from inside of the VM]({{< relref "Whats New/anka-2.5.5/index.md#anka-show-now-displays-cpu-usage-from-inside-of-the-vm" >}})
<!-- - **New Feature (experimental):** [Ability to separate runtime image from static image storage directories]({{< relref "Whats New/anka-2.5.5/index.md#ability-to-separate-runtime-image-from-static-image-storage-directories-experimental" >}}) -->

### 2.5.4 (2.5.4.138) - Dec 27th, 2021

{{< hint warning >}}

##### Important considerations for this release

- Upgrading Addons from the previous minor version of anka is recommended but not required.

- Suspended VMs created in previous _minor versions_ of anka are not compatible and will need to be force stopped (`anka stop --force`), started, and then re-suspended post-upgrade.


For more details, take a look at our [pre-upgrade considerations]({{< relref "intel/upgrading.md#pre-upgrade-considerations" >}}).
{{< /hint >}}

- **Bug Fix:** Automatic creation of anka image storage directories was not happening for config defaults and caused the agent to be unable to create VMs.

### 2.5.4 (2.5.4.136) - Dec 10th, 2021

{{< hint warning >}}

---

##### Important considerations for this release

- Upgrading Addons from the previous minor version of anka is recommended but not required.

- Suspended VMs created in previous minor versions of anka are not compatible and will need to be force stopped (`anka stop --force`), started, and then re-suspended post-upgrade.

- Avoid upgrading to this version on nodes with running VMs.


For more details, take a look at our [pre-upgrade considerations]({{< relref "intel/upgrading.md#pre-upgrade-considerations" >}}).
{{< /hint >}}

- **Bug Fix:** `anka list` was not sorted by name.
- **Bug Fix:** Race condition throws "not found" when `anka clone` and `anka delete` happen at the same time.
- **Bug Fix:** VMs created with the name "11.6" throw a failure.
- **Bug Fix:** Anka `registry list` command fails with `key values mismatch` when using self signed certs.
- **Bug Fix:** Machine readable `stop_date` is in a bad format for parsing (causing `day out of range`)
- **Bug Fix:** Machine readable status differ between `list` and `show` commands.
- **Bug Fix:** `anka create` suddenly throwing `hdiutil: attach failed - Resource busy` error.
- **Bug Fix:** `anka license show -k {license}` doesn't display proper host based license information.
- **Bug Fix:** Unable to use `change_res` binary on Big Sur, Monterey, and PG enabled VM templates.
- **Bug Fix:** On machine boot, `anka_agent` is running and executing `anka list` which triggers creation of *_lib directories. This was causing network mounts (which happen after the agent runs) to try using the same location, failing to because they already exist, and instead mounting with a different name. This caused `anka list` to be empty after a reboot. We removed the creation on `anka list` which will give enough time for network mounts to claim the path.
- **Bug Fix:** The anka uninstaller script was removing a locally installed controller package.
- **Improvement:** Monterey VM creation will automatically set `ablk` as the disk controller (`virtio-blk` not supported currently).
- **Improvement:** Support for 32 core machines.
- **Improvement:** We now check the registry status/availability before creating a local tag. This should prevent situations where a local tag was created prematurely and then blocked subsequent commands (requiring either a manual deletion of the local tag, or a force push).
- **New Feature:** [You can now find the last used date/time of a VM/Template using the `access_date` key/value.]({{< relref "Whats New/anka-2.5.4/index.md#ability-to-find-the-last-time-a-template-was-used" >}})
- This release includes support for 12.1 beta.

---

### 2.5.3 (2.5.3.135) - Sep 23rd, 2021

{{< hint warning >}}
Suspended VMs in 2.4.X are not compatible and will need to be force stopped (anka stop --force), started, and then re-suspended post-upgrade.
{{< /hint >}}

{{< hint info >}}
Upgrading Addons from the previous version of anka is recommended.
{{< /hint >}}

{{< hint warning >}}
Avoid upgrading the anka package to 2.5.X on nodes with VMs running.
{{< /hint >}}

- **Bug Fix:** Apple’s automatic software update/download is enabled for newly created VMs. This was causing a problem where the new macOS version installer .app was being downloaded each time a VM was started.
- **Bug Fix:** VMs randomly crashing with failed to get pid: Socket is not connected
- **Bug Fix:** anka config default_passwd returning 245 exit code
- **Bug Fix:** VM suspension logic was producing stopping VMs
- **Bug Fix:** Date strings in anka list have overflow in minutes and seconds fields

{{< hint warning >}}
Known issues we’re working on fixes for:

Creating a VM Template with the name of 11.6 seems to throw not found errors when trying to push, clone, etc.
{{< /hint >}}

---

### 2.5.2 (2.5.2.133) - Sep 13th, 2021

> Upgrading Addons from the previous version of anka is not necessary. We do however recommend upgrading addons if you're on a previous minor or major version of the CLI.

- Bug Fix: `anka list -f ram` was showing human readable values, vs the bytes output
- Bug fix: Addons < v2.3.X were not showing properly
- Bug Fix: Modifying network card was setting `no_local` to true
- Bug Fix: Updating addons on Mojave hosts was failing
- Bug Fix: PG enabled VMs were throwing failures on start
- Improvement: Deprecation notice added for `anka create --profile` as it no longer works on macOS versions greater than Catalina

> License pass-through for the Anka CLI is not longer available for VMs with Big Sur macOS or higher.

---

### 2.5.1 (2.5.1.132) - Aug 30th, 2021

> Upgrading Addons from the previous version is not necessary

- Bug Fix: `anka run --env` was not working
- Bug Fix: `anka list -f` was not working
- Bug Fix: `anka start --usb` was not working
- Bug Fix: `sudo anka view` was not working

---

### 2.5.0 (2.5.0.131) - Aug 19th, 2021

> Upgrading Addons from the previous version is recommended. Suspended VMs on 2.4.X seem to be problematic when starting on 2.5.X.

> 10.14.X does not contain the necessary Apple APIs to work with 2.5.X of Anka. You will need to upgrade macOS for your hosts to use 2.5.X.

- Bug Fix: Inability to create or start Anka VMs over SSH (no active UI) or as the ec2-user/non-root users on AWS EC2 Mac
- Bug Fix: Inability to run more than one VM on AWS EC2 Mac
- Bug Fix: Startup scripts through the controller API fail due to slow network/DHCP setup
- Bug Fix: Anka run doesn't source all available bash/profile source files for the user, only the first. It will now source all files in the following order: `/etc/profile`, `.bash_profile`, `.bash_login`, `.profile`.
- Improvement: Expanded Nested Virtualization to support Android Emulators and Virtualbox + refactored Docker support for modern macOS versions. **Nested Virtualization is only possible on Big Sur hosts and Big Sur or Catalina VM versions.** | [Documentation]({{< relref "intel/nested-virtualization.md" >}})
- Improvement: `anka show` now supports several new commands: `anka show {VMNAME} network`, `anka show {VMNAME} disk`, and `anka show {VMNAME} tags` | [Documentation]({{< relref "intel/Whats New/_index.md#additional-anka-show-commands" >}})
- Improvement: `anka show` is now possible for specific local tags | [Documentation]({{< relref "intel/Whats New/_index.md#additional-anka-show-commands" >}})
- Improvement: `anka delete {template}:{tag}` has been replaced with `anka delete {template} --tag {tag}` | [Documentation]({{ relref "intel/Whats New/_index.md#previous-tag-deletion-method-has-been-replaced" }})
- Improvement: You can now suspend VMs that have PG display enabled
- Improvement: `anka create` can now be done in multiple stages so MDM can target the VM to apply profiles on creation | [Documentation]({{< relref "intel/Whats New/_index.md#multi-stage-anka-create-for-mdm-profile-application" >}})
- New Feature: `anka stop` now detects if VM is unresponsive and issues forceful stop
- New Feature: Ability to control VM display frame rate with `anka modify {VMNAME} set display --fps 30` (defaults to 30) | [Documentation]({{< relref "intel/Whats New/_index.md#ability-to-control-vm-display-frame-rate" >}})
- New Feature: Monterey Beta VM support
- Fuse will no longer be installed within newly created VMs

> Known Issues we're working on fixes for:
> - Several command flags are not functioning properly in this version. Examples: `anka run --env/--env-file`, `anka start --usb/-d`, and `anka list -f`
> - `sudo anka view` or `anka view` as root seems to have stopped working.
> - `anka list -f ram` shows human readable values instead of bytes
> - `anka start -u` does not work on Mojave hosts

---

### 2.4.1 (2.4.1.130) - Apr 19th, 2021

> Upgrading Addons from the previous version is **NOT** necessary

- Improvement: Preliminary 11.3 support
- Bug Fix: Machine-readable output is sometimes empty
- Bug Fix: Block deallocation logic fails on some guest images
- Improvement: If available, `anka registry pull` will now revert to/use the local copy of your template/tag and avoid making a network pull/connection
- Improvement: If a template with a certain name exists on your machine/node, but doesn't match the UUID of the template with the same name in the registry, we are now blocking you from pulling the template from the registry to prevent duplicates
- New feature: `anka config` now contains `delete_logs` which, if set to False, will keep /Library/Logs/Anka/{UUID}.log files around even after deletion of the VM

---

### 2.4.0 (2.4.0.129) - Mar 31st, 2021

> Upgrading Addons from the previous version **is** necessary

- New Feature: (improved security) [VM network isolation when using shared type network-card]({{< relref "intel/Whats New/_index.md#vm-networking-is-now-isolated-for-improved-security" >}}). This also means that any access to the host also blocked (192.168.64.1).
- New Feature: [Pushing and pulling from the registry is now chunked]({{< relref "intel/Whats New/_index.md#registry-pushing-and-pulling-of-vm-templatestags-are-now-chunked-for-better-performance" >}}).
- Improvement: Suspended VMs that fail to start for a temporary issue will not become corrupted anymore. This allows a second start to happen without having to re-pull the suspended VM again from the registry.
- Improvement: Anka clone now preserves the source VM creation date.
- Bug Fix: Anka run suddenly throws `-anka: communication timeout`
- Bug Fix: When /var/tmp/ankafs.0 is created as one user, and another user in the VM tries to use it, it fails with `Permission Denied`
- Bug Fix: ENVs passing into the VM using `anka run --env` throw `-anka: communication timeout`
- Bug Fix: RealVNC client crash
- Bug Fix: Whenever multiple creations are run in parallel with packer, it will fail with `hdiutil: attach failed - Resource busy`

---

### 2.3.4 (2.3.4.128) - Mar 2nd, 2021

- Bug Fix: Default VNC (running on 590X ports) was frozen
- New Feature: Ability to set `anka modify VmName set network-card 0 --direct-mac` and expose the MAC address to the Host so that DHCP can assign the proper IP (requires bridged mode)

> Upgrading Addons from the previous version is **not** necessary

---

### 2.3.3 (2.3.3.127) - Feb 3rd, 2021

- Improvement: New low latency timer emulation logic (performance)
- Bug Fix: `anka cp` symlink copying produces corrupted links
- Bug Fix: VM resume instability
- Bug Fix: `ankanetd` was found to crash on older Mac Pros
- New Feature: License Fulfillment ID is now visible from `anka license show`
- New Feature: `anka config` options to modify Apple's mitigations on host.

> Please update addons for your Templates and Tags.

> NEW IN 2.3: `anka mount` and the automated current directory mounting for `anka run` are not available by default with Big Sur VMs. You can install addons using `anka start -o addons 11.0.X` and then choosing `Legacy addons` under the installer Options to enable them, but it requires manual approval/steps through the GUI.

> Known issue: 11.2 no longer supports the deprecated FUSE drivers. This could impact packer versions <= 1.6.1. Packer version 1.7.0 will support `anka cp` instead.

> Known issue: `anet` network card does not work for Big Sur VMs. You need to switch to `anka modify {vmName} set network-card -c virtio-net`

---

### 2.3.2 (2.3.2.125) - Jan 12th, 2021

- Improvement: Refined --help messages for CLI
- Improvement: VM Networking speeds and stability
- New Feature: Support for PG graphics ("Metal") devices in the VM
- Bug Fix: It's possible that the ankarund process can fail due to other software requesting access to usb devices inside of the VM. This was causing `anka run` to not function.
- Bug Fix: ENVs with special characters were causing `non CF convertable type passed` errors on the CLI.
- Bug Fix: `Failed to find bundle for accelerator bundle named: AnkaMTLDriver errno: 0` was displaying in simulator logs, causing CI/CD to fail. (addons update required)
- Bug Fix: 10.14 wasn't allowing nested virtualization
- Bug Fix: Running `anka --machine-readable license show` on a machine without a license throws an error

> Upgrading Addons from the previous version **is** necessary

> NEW IN 2.3: `anka mount` and the automated current directory mounting for `anka run` are not available by default with Big Sur VMs. You can install addons using `anka start -o addons 11.0.X` and then choosing `Legacy addons` under the installer Options to enable them, but it requires manual approval/steps through the GUI.

> Known issue: PG and Nested Virtualization are not compatible.

---
### 2.3.1 (2.3.1.124) - Dec 3rd, 2020

- New Feature: [You can now `anka delete {vmName}:{tagName}` in order to remove the tag LABEL from your VM. However, this does not remove the STATE of the tag from the VM, allowing you to create a new tag without losing the previous tag's config, installed dependencies, etc.]({{< relref "anka-virtualization-cli/getting-started/creating-vms.md#re-pushing-an-existing-registry-tag" >}})
- Bug Fix: Hostmachines running 10.13.6 were locking up when executing `anka run` and `anka cp` on them
- Bug Fix: Incorrect DHCP handling logic caused random IP to be assigned to VM
- Bug Fix: `anka modify set custom-variable sys.csr-active-config 0` doesn't work as expected

> NEW IN 2.3: `anka mount` and the automated current directory mounting for `anka run` are not available by default with Big Sur VMs. You can install addons using `anka start -o addons 11.0.X` and then choosing `Legacy addons` under the installer Options to enable them, but it requires manual approval/steps through the GUI.

---

### 2.3.0 (2.3.0.122) - Nov 24, 2020

- New Feature: A free, but limited, license for developers and small teams (on by default)
- New Feature: Anka App now has a management UI where you can stop, start, delete, and create VMs
- New Feature: Anka Viewer now prompts you, when you try to close the window, whether you want to stop the VM or keep it running in the background
- New Feature: anka create support for Big Sur (avoiding having to upgrade Catalina)
- New Feature: `anka cp` is replacing our older `anka mount` and automatic mounting for `anka run` due to changes Apple has made in Big Sur.
- New Feature: Ability to control hostname inside of VM with `propagate_name` config option and `ANKA_HOSTNAME` env variable
- New Feature: Bridged network modes now support VLANs with the `anka modify --vlan` option
- Change: `anka create` default CPU, RAM, and DISK are now:
    - CPU: (totalVirtualCPUCount / 2) with a min of 2 and a max of 8
    - RAM: (totalRamAvailable / 2) with a min of 2GB and a max of 8GB
    - DISK: 128G (137438953472)
    > Configurable with `anka config`
- Bug Fix: Suspending a VM with a mounted disk (`anka start -o`) will cause it to fail on boot
- Bug Fix: Inability to interrupt `anka registry pull`
- Bug Fix: License activation didn't work on Big Sur host
- Bug Fix: Reboots from within VM sometimes show a black screen
- Bug Fix: Unable to upgrade 10.14 VM to 10.14.1

> NEW IN 2.3: `anka mount` and the automated current directory mounting for `anka run` are not available by default with **Big Sur VMs**. You can install addons using `anka start -o addons 11.0.X` and then choosing `Legacy addons` under the installer Options to enable them, but it requires manual approval/steps through the GUI. Catalina will still receive the older drivers.

> Known Issues:
> 
> 1. With Big Sur VMs, DHCP/IP assignment seems flakey and will cause a random IP to be applied.

---

### 2.2.3 (2.2.3.118) - May 03, 2020
- Bug Fix: Starting multiple VMs from suspended state with bridge networking configuration
- Bug Fix: Unable to set up port forwarding to 127.0.0.1
- Bug Fix: VNC connection error
- Bug Fix: DHCP bug related to renew lease in some Anka environment
- Bug Fix: anka VMs can get corrupted when using nanka kext in cases of force shutdown
- Bug Fix: Trying to start a VM result in failed state - with logs saying bind: Address already in use
- New Feature: When using Anka Viewer, after clicking the green full screen button on the window's top bar, it's unclear how to get out of full screen. Now, if you move your mouse to the top of the screen you will expose the bar and green button.
- New Feature: Updated license terms

    > There is no requirement to upgrade the VM templates from previous anka version 2.2.2 to version 2.2.3.

---

### 2.2.2 - Mar 03, 2020
- Bug Fix: Nested virtualization not working since rel 2.2.0
- Bug Fix: Anka command failed: time data ‘2020-02-27T03:52:23Z’ does not match format ‘%d %b %Y %H:%M:%S’
- Bug Fix: license pass-through from root VM to nested VM doesn't work
- Bug Fix: anka run sources both .bash_profile and .profile. Requires`anka start -u` for existing VM templates.
- Bug Fix: after rebooting a running vm with anka run VM sudo reboot`,  network doesn't work.
- New Feature: Allow to specify display physical(DPI) parameters. Requires `anka start -u` for existing VM templates.

> There is no need to upgrade the VM templates from previous anka version 2.2.1 to version 2.2.2, unless you need to use the items from the above list which explicitly state the requirement of `anka `.

---

### 2.2.2 - Mar 03, 2020
- Bug Fix: Nested virtualization not working since rel 2.2.0
- Bug Fix: Anka command failed: time data ‘2020-02-27T03:52:23Z’ does not match format ‘%d %b %Y %H:%M:%S’
- Bug Fix: license pass-through from root VM to nested VM doesn't work
- Bug Fix: anka run sources both .bash_profile and .profile. Requires`anka start -u` for existing VM templates.
- Bug Fix: after rebooting a running vm with anka run VM sudo reboot`,  network doesn't work.
- New Feature: Allow to specify display physical(DPI) parameters. Requires`anka start -u` for existing VM templates.

---

### 2.2.1 - Feb 24, 2020
- Bug Fix: RFB server crash 0x0000000104fa0b8c rfb_thr + 1364
- Bug Fix: Crash on suspend
- Bug Fix: ankactl doesn't report vnc_password string
- Bug Fix: Anka VM fails to start under jenkins master account
- Bug Fix: Anka run --wait-network doesn't seem to work
- Bug Fix: set resolution from anka view doesn't work.
- Bug Fix: Anka version takes a few minutes to respond
- Bug Fix: ankactl experiences EMFILE if there are many snapshots/vms in the library
- Bug Fix: Adding MAC address using anka modify for bridge cards result in corrupted config file for VM
- Bug Fix: Collision of anka and guest addons files
- Bug Fix: VNC not working for when resolution of VM is changed to 1000*600
- Bug Fix: Problems to detect IP address
- Bug Fix: VM doesn't get unique IP address if static MAC address specified
- New Feature: Support IPv6 in anka rfb server
- New Feature: Allow to assign MAC address to VM
- New Feature: Create directories if missing with anka run --workdir (requires anka start -u)
- New Feature: Send HID events programmatically (requires anka start -u)
- New Feature: Create RFB threads on demand only
- New Feature: Give proper message in case of a VM trying to access out of range memory

---

### 2.2.0 - Jan 10, 2020
- Bug Fix: vmnet fails to create interface
- Bug Fix: Network error (discovered while stress testing)
- Bug Fix: anka clone doesn’t randomize MAC addresses
- Bug Fix: Samsung Galaxy S9 claim leads to host panic
- Bug Fix: anka registry pull doesn’t take in scope cache size when determining free space
- Bug Fix: nvram values don’t get saved
- Bug Fix: Not possible to start more than one VM without GUI session
- Bug Fix: vmnet fails to create more than few instances of virtual interfaces without GUI session
- Bug Fix: Exceeding host based license message is missleading
- Bug Fix: mDNS requests looks fail from inside VM
- Bug Fix: Shared folders work bad for GUI usecases
- Bug Fix: vmnet doesn’t restore network connectivity after host sleep
- Bug Fix: Android devices aren’t recognized in Android Studio
- Bug Fix: The source command doesn’t pickup changes in PATH environment. (requires anka start -u for the VMs)
- Bug Fix: Anka.pkg downgrades AnkaAgent.pkg
- Bug Fix: Bad product type for Anka Build Lite
- Bug Fix: Anka run --wait-network doesn’t seem to work
- New Feature: Install AnkaView into /Applications
- New Feature: Allow to modify networking type of suspended VM
- New Feature: Allow to create VM with manual install process
- New Feature: Allow to start VMs via AnkaView interface
- New Feature: Support output fields list customization
- New Feature: Implement bridge support with new vmnet functionality
- New Feature: Allow to claim/release USB devices by Serial Number
- New Feature: Allow to select the bridge interface automatically
- New Feature: MAC address sync
- New Feature: Static IP addresses support (requires anka start -u for the VMs)
- New Feature: Performance optimization
- Other: Remove vlaunch
- Other: Move ankanetd service to unix domain
- Other: Allow to create more than 4 anka vmnet interfaces
- Other: Integrate new VTUFS 3.10.4 (requires anka start -u for the VMs)
- Other: Changes to licenses

---

### 2.1.2 - Oct 10, 2019
- Bug Fix: SSH is not turned ON by default on Catalina guests

---

### 2.1.1 - Sep 25, 2019
- Bug Fix: networking in Anka VMs doesn't work in Catalina beta 8. User reported issue.
- Bug Fix: License auto renewal doesn't work.
- Bug Fix: anka run -N sometimes fail to wait for network properly.

---

### 2.1.0 - Aug 21, 2019
- Bug Fix: Starting VM with USB device could interfere with previously assigned device
- Bug Fix: Anka View doesn't allow to drag with mouse
- Bug Fix: Guest hangs after host sleep
- Bug Fix: Shared folders doesn't work on Catalina
- Bug Fix: Pasteboard policy isn't indicated in GUI
- Bug Fix: Anka Secure license is being processes with core rules
- Bug Fix: Kernel panic in VeertuNet
- Bug Fix: anka stop doesn't trim encrypted drives
- Bug Fix: Display doesn't return to full screen after restart
- Bug Fix: Pasteboard policy isn't indicated in GUI
- New Feature: Support hot plug of USB devices
- New Feature: Allow to specify relative paths in anka run -w option
- New Feature: Allow to control pb paste and copy operations independently
- New Feature: Updated EULA and acknowledgements

---

### 2.0.1
- Supports multiple license types for different products. Anka Build Basic, Anka Build Enterprise, Anka Build Enterprise Plus, Anka Flow, Anka Secure
- Bug Fix: Catalina beta 3 reboot/start error on anka create
- Bug Fix: Anka Flow license uses core based fulfillments
- Bug Fix: anka license show crashes
- Bug Fix: Same IP address is being assigned to bridged VMs
- Bug Fix: mmap files are not being deleted

---
### 2.0
- Bug Fix: Sometimes VM fails to resume with error accessing state file
- Bug Fix: Bad serialization to YAML
- Bug Fix: Suspend failed
- Bug Fix: Anka view crashes on copy/paste operation
- Bug Fix: Hang on resume
- Bug Fix: macOS boot stuck sometimes
- Bug Fix: Problem in image/state deletion
- Bug Fix: Unaligned disk access
- Bug Fix: Guest kernel panic
- Bug Fix: Anka View Crash
- Bug Fix: libosxfuse has loading problems due to Library Validation
- Bug Fix: RealVNC client crashes ankahv
- Bug Fix: Berry doesn't load on 10.12
- Bug Fix: Guest kernel panics on resume
- Bug Fix: Can't attach more than one USB device
- Bug Fix: Uhost craches sometimes leaving the device busy
- Bug Fix: Ankahv crashes on sharedfs operation
- Bug Fix: subsequent clone/delete commands leave unreferenced state files
- Bug Fix: User reported permission problem in anka create -a
- Bug Fix: Tar fails to update modification date of symlinks over sharedfs
- Bug Fix: Guest reboots during the installation of Homebrew
- Bug Fix: During CI it's observed an increased number of guest panics
- Bug Fix: Anka registry add doesn't work with self-signed certificates
- Bug Fix: Ankahv crashes in xhci module
- Bug Fix: Deadlock on boot
- Bug Fix: Anka exception on registry operation
- Bug Fix: Anka trust insecure registry
- Bug Fix: Inefficient suspend
- Bug Fix: 1.4 suspended Vm fails to start in 1.5(internal release)
- Bug Fix: Anka view on 1.4 VM in 1.5(internal release) shows a black border at the bottom
- Bug Fix: VM became stopped on suspend
- Bug Fix: Anka usb list fails on new MBP2018
- Bug Fix: Installation of macOS guest hangs in the middle
- Bug Fix: Ios emulator fails to run
- Bug Fix: Ios emulator causes a triple fault with nAnkaVM driver loaded and nanka engine
- Bug Fix: Double cursor is displayed in anka view
- Bug Fix: Anka vm doesn't have networking after first boot (only after a reboot)
- Bug Fix: Long running VMs crashing (probably due to resources/memory overallocation)
- Bug Fix: Policy functionality is broken in very latest versions of Anka (Anka Secure Product related)
- Bug Fix: Anka does not start the graphics driver with correct arguments
- Bug Fix: Anka clone operation doesn't check for policy rules producing unstartable VMs in negative scenario (Anka Secure Product related)
- Bug Fix: Guest macOS v10.12 hangs on boot on Berry load
- Bug Fix: License activation detecting 8core imac as 4 core
- Bug Fix: After creating sierra VM network driver not loaded
- Bug Fix: Enable policy without forcing user to stop VM (Anka Secure Product related)
- Bug Fix: Vcpu_lock() deadlock
- Bug Fix: Anka registry pull fails due to missing of policy file (Anka Secure Product related)
- Bug Fix: Anka registry add doesn't work with certificates
- Bug Fix: Latest controller fails to start VM
- Bug Fix: Issue with the registry for mac summary window during install
- Bug Fix: Anka registry does not return right error for 403
- Bug Fix: Swift build fails over a shared folder
- Bug Fix: Switching to Keylocked Anka View (with e.g. Cmd+Tab) leaves the keys pressed on host side time to time
- Bug Fix: osxfuse 3.3 (used currently) is not fully compatible with 10.14
- Bug Fix: Uhost fails to pass-through some USB devices
- Bug Fix: Anka View (2.0) crashed during live resize
- Bug Fix: Host not reporting CPu core count during renewal/license exp call. previous core count is being overwritten.
- Bug Fix: Installer hangs on 10.15 beta
- Bug Fix: Ankactl crashes on start, stop, show operations on 10.15 beta
- Bug Fix: AnkaView shows white box in 10.15 beta
- Bug Fix: Anka create fails to create/configure the default user
- Bug Fix: Image that was suspended for longer than 1 hour does not work in 10.15 beta VMs.
- Bug Fix: "Anka View quit unexpectedly" when I turned off the VM through the Apple menu
- Bug Fix: Failed to assign 256 bytes of key data, error 0
- Bug Fix: Pull operation doesn't update policy file reference in VM object (Anka Secure Product related)
- Bug Fix: Fix typos
- Bug Fix: Long boot of 10.15 beta
- Bug Fix: Anka --debug registry pull --shrink issue
- Bug Fix: Bad messaging for registry operations if no registry configured
- Bug Fix: Better UID/permissions support in shared folders
- New Feature: Massive performance optimizations
- New Feature: Catalina VM support
- New Feature: Secure controllable VM environments (Anka Secure Product related)
- New Feature: New AnkaView application with multi-display support
- New Feature: Unified Anka package
- New Feature: Allow extending existing ANKA images
- New Feature: New anka view screenshot command form
- New Feature: Disable network discovery to prevent duplicate name dialogs
- New Feature: Detect ssh session in anka view and inform the user about vnc
- New Feature: Limit Anka View window size by desktop visible area
- New Feature: Allow connecting multiple USB devices to VM
- New Feature: Better TLS support in anka registry 
- New Feature: Ability to encrypt VNC password
- New Feature: OpenID connect login support for anka registry
- New Feature: Show creation/start/stop dates of VM
- New Feature: Added ability to passthru/configure PlatformID and Serial Number to the VM 
- New Feature: Show  license fulfillment information associated with a key with anka license command
