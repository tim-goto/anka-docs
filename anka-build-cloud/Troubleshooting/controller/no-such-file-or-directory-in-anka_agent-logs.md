---
title: "No such file or directory in anka_agent logs"
linkTitle: "No such file or directory in anka_agent logs"
weight: 1
---

## Scenario

If you use a custom *lib config location, and have not created or run a VM before on a machine, trying to pull a VM from the registry through the Anka Agent will error out in the logs like:

```bash
I1214 22:57:11.857070     615 start_vm.go:217] checking for disk space
E1214 22:57:12.714660     615 start_vm.go:44] [Errno 2] No such file or directory: '/storage/img_lib/'
I1214 22:57:12.725765     615 start_vm.go:36] started handling startVMRequest
```

## Solution

Create the directories `sudo mkdir -p "$(sudo anka config img_lib_dir)" && sudo mkdir -p "$(sudo anka config state_lib_dir)" && sudo mkdir -p "$(sudo anka config vm_lib_dir)"`.

## Still experiencing problems?

Talk to us! we are available via [slack](https://slack.veertu.com/) or [email](mailto:support@veertu.com)
