# pt_mode

This repository provides a Linux kernel module and the companion proxy application. It also provides helper scripts to build modified glibc and [patchelf](https://github.com/NixOS/patchelf) to patch target COTS binaries. The most part of the code originates from [junxzm1990/afl-pt](https://github.com/junxzm1990/afl-pt) and [AFL++ CoreSight mode](https://github.com/AFLplusplus/AFLplusplus/tree/stable/coresight_mode). The fuzzuf PT Executor depends on this repository.

## Building

To build the Linux kernel module and the proxy applications, run:

```shell
make build
```

This make command will build `ptmodule/ptmodule.ko`, `pt_proxy/afl-pt-proxy` and `pt_proxy/pt-proxy-fast`.

## Usage

### Patch COTS Binary

The proxy application only supports fork server mode, which requires patchelf and the patched glibc. The below make command builds the dependency build:

```shell
make patch TARGET=$BIN
```

The above command builds and installs the dependencies to `$PREFIX` (default to `$PWD/.local`) for the first time. Then, it runs `patchelf` to `$BIN` with output `$OUTPUT` (`$BIN.patched` by default).

### Install `ptmodule.ko`

The proxy application requires the target environment to the `ptmodule.ko` installed:

```shell
cd ptmodule
./reinstall_ptmod.sh
```

## License

This repository is released under the [GNU General Public License v3.0](/LICENSE). Some parts of the external source code are licensed under their own licenses.
