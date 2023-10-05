## Intro

This project is a simple hello-world made with [ebpf](https://ebpf.io).


It is composed by a C file listening to the execve syscall. When it happens, it just print "hello world".
It also has a Golang part, that load the bpf program and trigger the execve syscall by running `ls`.

Finally, a Taskfile was made to make it easier to orchestrate this mess.


## Things to know.

- It was created on ubuntu, which has a little caveat : the `asm/types.h` header file needed by one of the bpf C lib is located in a specific place that need to be explicitly include at compilation time.
- It needs to be run with sudo (the run task does this for you).
- If you want to use the task in the taskfile, you need to install [taskfile](https://taskfile.dev/) first.
- In order to see the `hello world` message appear, you need to `cat` on `sys/kernel/debug/tracing/trace_pipe` (need to be run as sudo/root) since the C program use `bpf_trace_printk`.
