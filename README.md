# imcpy
Python bindings for [Inter-Module Communication Protocol (IMC)](https://lsts.fe.up.pt/toolchain/imc) used to communicate between modules in the [LSTS toolchain](https://lsts.fe.up.pt/).

## Requirements for building

- Linux-based host operating system is required.
- git
- python3

## Installation

### Source install

#### Clone the project recursively
```bash
git clone --recursive git@github.com:oceanscan/imcpy-omst.git
```
This includes the pybind11 submodule.

#### If using OMST IMC repo with DUNE from LSTS, remove the following lines from dune/cmake/IMC.cmake (this is required because the IMC from OMST does not include a IMC_Addresses.xml file)
```cmake
      COMMAND ${DUNE_PROGRAM_PYTHON}
      ${PROJECT_SOURCE_DIR}/programs/generators/imc_addresses.py
      ${extra_flags}
      -x ${DUNE_IMC_ADDRESSES_XML} ${PROJECT_SOURCE_DIR}/etc/common/imc-addresses.ini
```

#### Build and install the library

```bash
pip3 install .
```

If you use the system python and only want to install for a single user, you can add --user to the install command without needing administrator rights. On Windows, the Windows SDK must be installed with Visual Studio and the CMake executable must be on the system PATH.

##### (Optional) Use a specific IMC/Dune version
Replace the dune/imc submodules with the target versions

##### (Optional) Only generate bindings for a subset of IMC messages
A config file named whitelist.cfg can be placed in the root folder to
only create bindings for a subset of the IMC messages. This can be necessary when compiling on
embedded systems, as the linker consumes much memory for the full message set.
If an unknown message is parsed, it will be returned as the Message baseclass rather than a specialized message.
Look at minimal_whitelist.cfg for a set of messages that should always be included.

#### Recommendations
- The imcpy library generates stub files for the bindings, meaning that you can have autocomplete and static type checking if your IDE supports them. This can for example be [PyCharm](https://www.jetbrains.com/pycharm/) or [Jedi](https://github.com/davidhalter/jedi)-based editors.
