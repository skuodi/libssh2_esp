<div align="center">

[![GitHub release](https://img.shields.io/github/release/skuodi/libssh2_esp?include_prereleases=&sort=semver&color=brightgreen)](https://github.com/skuodi/libssh2_esp/releases/)
[![License](https://img.shields.io/badge/License-BSD--3--Clause-brightgreen)](#license)

# libssh2_esp

> libssh2 + ESP-IDF

</div>

A port of [libssh2-1.11.1](https://github.com/libssh2/libssh2/tree/libssh2-1.11.1) as an ESP-IDF component.
The library itself is included unmodified as a git submodule in the
`libssh2` directory. [An example](examples/ssh2_exec) is provided to
demonstrate using SSH to run a command on a remote server.

## Usage

1. As a ESP-IDF managed component: In your project directory run

```
idf.py add-dependency skuodi/libssh2_esp==1.1.0
```

2. As a git submodule: In your project, `components/` directory, run

```
git submodule add https://github.com/skuodi/libssh2_esp.git
git submodule update --init --recursive
```

The library can be configured via `idf.py menuconfig` under `Component config` > `libssh2`.

## Examples

- [ssh2_exec](examples/ssh2_exec) - run the `ls` command at [bandit.labs.overthewire.org](https://overthewire.org/wargames/bandit/bandit0.html).

![ssh2_exec](examples/ssh2_exec/run.gif)

## Porting notes

The configuration of this component in ESP-IDF menuconfig is located under
`Component config` > `libssh2` where the `Compile libssh2 with debug logging`
option can be enabled to compile debug log functions into the final binary.<br>
With the logging functions included in compiation,
`libssh2_trace(session, bitmask)` must be called at runtime to select the
phases of the SSH operation for which to enable logging. See the example in
[ssh2_exec.c](examples/ssh2_exec/main/ssh2_exec.c#L397).<br>

The cryptography engine used by libssh2 may also be set under
`Component config` > `libssh2`  > `Cryptography engine`, though the only one
currently supported is `mbedTLS` which comes bundled into ESP-IDF by default.

## License

Released under [BSD-3-Clause](/LICENSE) by [@skuodi](https://github.com/skuodi).
