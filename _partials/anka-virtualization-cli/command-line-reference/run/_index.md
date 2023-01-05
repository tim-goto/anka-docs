```shell
> anka run --help
usage: run [options] vmid

   Run a command inside of a VM

arguments:
  vmid                     VM name or identifier (will be started if needed)

options:
  -D,-w,--workdir <val>    Working directory inside the VM
  -v,--volume <val>        Mount a host directory into VM
  -n,--no-volume           Prevent implicit mounting of current folder (see --volume option)
  -E                       Inherit the entire environment in non-overriding mode
  -e <val>                 Provide an environment variable in overriding mode
  -f,--env-file <val>      Provide environment variables from file
  -q,--quiet               Suppress the stdout from the command
  -b,--background          Run the command in background returning PID to wait with 'wait [PID...]' command
```
