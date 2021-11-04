# bazel-issue-14226

This repository contains a minimal example of the issue described in:
https://github.com/bazelbuild/bazel/issues/14226

To replicate the issue, run `bazel build //:example --sandbox_debug`.

This will yield an error similar to the following:
```
$ bazel build //:example --sandbox_debug
INFO: Analyzed target //:example (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: /home/pras/bazel-hermetic-sandbox/BUILD.bazel:1:11: Compiling example.cpp failed: (Exit 1): linux-sandbox failed: error executing command 
  (cd /home/pras/.cache/bazel/_bazel_pras/f17e96032b46eeff7d13f6f3fa1af6a3/sandbox/linux-sandbox/5/execroot/bazel_hermetic_sandbox && \
  exec env - \
    PATH=/home/pras/.cache/bazelisk/downloads/bazelbuild/bazel-6.0.0-pre.20211025.1-linux-x86_64/bin:/home/pras/.krew/bin:/home/pras/.nvm/versions/node/v12.18.3/bin:/home/pras/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin \
    PWD=/proc/self/cwd \
    TMPDIR=/tmp \
  /home/pras/.cache/bazel/_bazel_pras/install/850276ae221e5ad4603a47e9b49bd43a/linux-sandbox -t 15 -w /home/pras/.cache/bazel/_bazel_pras/f17e96032b46eeff7d13f6f3fa1af6a3/sandbox/linux-sandbox/5/execroot/bazel_hermetic_sandbox -w /tmp -w /dev/shm -M / -h /home/pras/.cache/bazel/_bazel_pras/f17e96032b46eeff7d13f6f3fa1af6a3/sandbox/linux-sandbox/5 -D -- /usr/bin/gcc -U_FORTIFY_SOURCE -fstack-protector -Wall -Wunused-but-set-parameter -Wno-free-nonheap-object -fno-omit-frame-pointer '-std=c++0x' -MD -MF bazel-out/k8-fastbuild/bin/_objs/example/example.pic.d '-frandom-seed=bazel-out/k8-fastbuild/bin/_objs/example/example.pic.o' -fPIC -iquote . -iquote bazel-out/k8-fastbuild/bin -fno-canonical-system-headers -Wno-builtin-macro-redefined '-D__DATE__="redacted"' '-D__TIMESTAMP__="redacted"' '-D__TIME__="redacted"' -c example.cpp -o bazel-out/k8-fastbuild/bin/_objs/example/example.pic.o)
1636050087.194696190: src/main/tools/linux-sandbox.cc:152: calling pipe(2)...
1636050087.194748260: src/main/tools/linux-sandbox.cc:171: calling clone(2)...
1636050087.195282399: src/main/tools/linux-sandbox.cc:180: linux-sandbox-pid1 has PID 13827
1636050087.195306567: src/main/tools/linux-sandbox-pid1.cc:641: Pid1Main started
1636050087.195425296: src/main/tools/linux-sandbox.cc:197: done manipulating pipes
1636050087.196284581: src/main/tools/linux-sandbox-pid1.cc:580: mount: /

1636050087.196513283: src/main/tools/linux-sandbox-pid1.cc:609: writable: /home/pras/.cache/bazel/_bazel_pras/f17e96032b46eeff7d13f6f3fa1af6a3/sandbox/linux-sandbox/5/execroot/bazel_hermetic_sandbox
src/main/tools/linux-sandbox-pid1.cc:612: "mount(/home/pras/.cache/bazel/_bazel_pras/f17e96032b46eeff7d13f6f3fa1af6a3/sandbox/linux-sandbox/5/execroot/bazel_hermetic_sandbox, /home/pras/.cache/bazel/_bazel_pras/f17e96032b46eeff7d13f6f3fa1af6a3/sandbox/linux-sandbox/5/execroot/bazel_hermetic_sandbox, nullptr, MS_BIND | MS_REC, nullptr)": No such file or directory
1636050087.214234533: src/main/tools/linux-sandbox.cc:233: child exited normally with code 1
Target //:example failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 0.193s, Critical Path: 0.03s
INFO: 2 processes: 2 internal.
FAILED: Build did NOT complete successfully
```
