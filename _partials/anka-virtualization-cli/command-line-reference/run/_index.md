```shell
> anka run --help
usage: run [options] vmid

   Run a command inside of a VM

arguments:
  vmid                     VM name or identifier (will be started if needed)

options:
  -D,-w,--workdir <val>    Working directory inside the VM
  -E                       Inherit the entire environment in non-overriding mode
  -e <val>                 Provide an environment variable in overriding mode
  -f,--env-file <val>      Provide environment variables from file
  -q,--quiet               Suppress the stdout from the command
  -b,--background          Background the command inside of VM, returning inner VM PID
```
