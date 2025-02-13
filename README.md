# nRF Connect SDK Example Application

This repository contains an nRF Connect SDK (NCS) example application. The main
purpose of this repository is to serve as a reference on how to structure Zephyr
based applications. Some of the features demonstrated in this example are:

- Basic [Zephyr application][app_dev] skeleton
- [Zephyr workspace applications][workspace_app]
- [West T2 topology][west_t2]
- [Custom boards][board_porting]
- Custom [devicetree bindings][bindings]
- Out-of-tree [drivers][drivers]
- Out-of-tree libraries
- Example CI configuration (using Github Actions)
- Custom [west extension][west_ext]

This repository is versioned together with the [NCS main tree][sdk-nrf]. This
means that every time that NCS is tagged, this repository is tagged as well
with the same version number, and the [manifest](west.yml) entry for `zephyr`
will point to the corresponding NCS tag. For example, `example-application`
v2.6.0 will point to NCS v2.6.0. Note that the `main` branch will always
point to the development branch of NCS, also `main`.

[app_dev]: https://docs.zephyrproject.org/latest/develop/application/index.html
[workspace_app]: https://docs.zephyrproject.org/latest/develop/application/index.html#zephyr-workspace-app
[west_t2]: https://docs.zephyrproject.org/latest/develop/west/workspaces.html#west-t2
[board_porting]: https://docs.zephyrproject.org/latest/guides/porting/board_porting.html
[bindings]: https://docs.zephyrproject.org/latest/guides/dts/bindings.html
[drivers]: https://docs.zephyrproject.org/latest/reference/drivers/index.html
[sdk-nrf]: https://github.com/nrfconnect/sdk-nrf
[west_ext]: https://docs.zephyrproject.org/latest/develop/west/extensions.html

## Getting Started

Before getting started, make sure you have a proper Zephyr development
environment. You can follow the official
[NCS Getting Started Guide](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/getting_started.html).

### Initialization

The first step is to initialize the workspace folder (``my-workspace``) where
the ``example-application`` and all NCS modules will be cloned. You can do
that by running:

```shell
# initialize my-workspace for the example-application (main branch)
west init -m https://github.com/nrfconnect/example-application --mr main my-workspace
# update NCS modules
cd my-workspace
west update
```

### Build & Run

The application can be built by running:

```shell
west build -b $BOARD app
```

where `$BOARD` is the target board. The `custom_plank` board found in this
repository can be used. Note that NCS sample boards may be used if an
appropriate overlay is provided (see `app/boards`).

A sample debug configuration is also provided. You can apply it by running:

```shell
west build -b $BOARD app -- -DOVERLAY_CONFIG=debug.conf
```

Note that you may also use it together with `rtt.conf` if using Segger RTT. Once
you have built the application you can flash it by running:

```shell
west flash
```
