## Building:

At the time of writing, runc only builds on the Linux platform.

```bash
# create a 'github.com/opencontainers' in your GOPATH/src
cd github.com/opencontainers
git clone https://github.com/opencontainers/runc
cd runc
make
sudo make install
```

In order to enable seccomp support you will need to install libseccomp on your
platform. If you do not with to build `runc` with seccomp support you can add
`BUILDTAGS=""` when running make.

#### Build Tags

`runc` supports optional build tags for compiling in support for various
features.


| Build Tag | Feature                            | Dependency  |
|-----------|------------------------------------|-------------|
| seccomp   | Syscall filtering                  | libseccomp  |
| selinux   | selinux process and mount labeling | <none>      |
| apparmor  | apparmor profile support           | libapparmor |

## Testing:

You can run tests for runC by using command:

```bash
# make test
```

Note that test cases are run in Docker container, so you need to install
`docker` first. And test requires mounting cgroups inside container, it's
done by docker now, so you need a docker version newer than 1.8.0-rc2.

You can also run specific test cases by:

```bash
# make test TESTFLAGS="-run=SomeTestFunction"
```