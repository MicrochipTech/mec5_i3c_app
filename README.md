# Zephyr Example Application for MEC1753 I3C

<a href="https://github.com/zephyrproject-rtos/example-application/actions/workflows/build.yml?query=branch%3Amain">
  <img src="https://github.com/zephyrproject-rtos/example-application/actions/workflows/build.yml/badge.svg?event=push">
</a>
<a href="https://github.com/zephyrproject-rtos/example-application/actions/workflows/docs.yml?query=branch%3Amain">
  <img src="https://github.com/zephyrproject-rtos/example-application/actions/workflows/docs.yml/badge.svg?event=push">
</a>
<a href="https://github.com/MicrochipTech/mec5_i3c_app">
  <img alt="Documentation" src="https://img.shields.io/badge/documentation-3D578C?logo=sphinx&logoColor=white">
</a>
<a href="https://zephyrproject-rtos.github.io/example-application/doxygen">
  <img alt="API Documentation" src="https://img.shields.io/badge/API-documentation-3D578C?logo=c&logoColor=white">
</a>

This repository contains a Zephyr sample application for Microchip's MEC1753 
I3C peripheral. It is based on the Zephyr example application framework.
Some of the features demonstrated in this example are:

- Basic [Zephyr application][app_dev] skeleton
- [Zephyr workspace applications][workspace_app]
- [Zephyr modules][modules]
- [West T2 topology][west_t2]
- [Custom boards][board_porting]
- Custom [devicetree bindings][bindings]
- Out-of-tree [drivers][drivers]
- Out-of-tree libraries
- Example CI configuration (using GitHub Actions)
- Custom [west extension][west_ext]
- Doxygen and Sphinx documentation boilerplate

This repository is versioned together with the Microchip fork of the 
[Zephyr main tree][zephyr] and [hal_microchip].

[app_dev]: https://docs.zephyrproject.org/latest/develop/application/index.html
[workspace_app]: https://docs.zephyrproject.org/latest/develop/application/index.html#zephyr-workspace-app
[modules]: https://docs.zephyrproject.org/latest/develop/modules.html
[west_t2]: https://docs.zephyrproject.org/latest/develop/west/workspaces.html#west-t2
[board_porting]: https://docs.zephyrproject.org/latest/guides/porting/board_porting.html
[bindings]: https://docs.zephyrproject.org/latest/guides/dts/bindings.html
[drivers]: https://docs.zephyrproject.org/latest/reference/drivers/index.html
[zephyr]: https://github.com/MicrochipTech/zephyr
[hal_microchip]: https://github.com/MicrochipTech/hal_microchip
[west_ext]: https://docs.zephyrproject.org/latest/develop/west/extensions.html

## Getting Started

Before getting started, make sure you have a proper Zephyr development
environment. Follow the official
[Zephyr Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html).

### Initialization

The first step is to initialize the workspace folder (``zws``) where
the ``mec5_i2c_app`` and all Zephyr modules will be cloned. Run the following
command:

```shell
# initialize zws for the mec5_i3c_app (main branch)
mkdir ~/zws
# configure a python virtual environment in zws
python -m venv ~/zws/.venv
# enter the python virtual environment
source ~/zws/.venv/bin/activate
cd ~/zws
# install west and other python modules
pip install west
pip install unidiff
pip install compdb
# Download the mec5_i3c_app using https or GitHub tool (gh)
git clone https://github.com/MicrochipTech/mec5_i3c_app
# or using GitHub command line tools assuming you have authentication configured
gh repo clone MicrochipTech/mec5_i3c_app
# Intialize the local repo
west init -l mec5_i3c_app
# Update to pull down the Zephyr, Microchip HAL, and CMSIS HAL.
west update
west zephyr-export
# Download Pythom modules required by Zephyr
pip install -r ~/zws/zephyr/scripts/requirements.txt
```

### Building and running

To build the application, run the following command:

```shell
cd mec5_i3c_app
west build -p always -b mec_assy6941_mec1753qsz app
```

One can define the environment variable BOARD=mec_assy6941_mec1753qsz and use
$BOARD in commands

NOTE: mec5_i3c_app contains the 'custom_plank` board which is present only
as a reference on how to implement an out-of-tree board. It is not meant
to build with the I3C application.

A sample debug configuration is also provided. To apply it, run the following
command:

```shell
west build -b $BOARD app -- -DEXTRA_CONF_FILE=debug.conf
```

### Testing

To execute Twister integration tests, run the following command:

```shell
west twister -T tests --integration
```

### Documentation

A minimal documentation setup is provided for Doxygen and Sphinx. To build the
documentation first change to the ``doc`` folder:

```shell
cd doc
```

Before continuing, check if you have Doxygen installed. It is recommended to
use the same Doxygen version used in [CI](.github/workflows/docs.yml). To
install Sphinx, make sure you have a Python installation in place and run:

```shell
pip install -r requirements.txt
```

API documentation (Doxygen) can be built using the following command:

```shell
doxygen
```

The output will be stored in the ``_build_doxygen`` folder. Similarly, the
Sphinx documentation (HTML) can be built using the following command:

```shell
make html
```

The output will be stored in the ``_build_sphinx`` folder. You may check for
other output formats other than HTML by running ``make help``.
