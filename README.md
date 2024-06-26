
<p align="center">
  <img src="https://github.com/BHare1985/mosaic/assets/2180284/73ac71af-2309-4efd-a24a-bf8d8b021eb1" height="384" width="auto" />
</p>

# Mosaic - Decentralized Data Parity Broker

This project aims to revolutionize data distribution using a high-performant distribution of verifiable and repairable fountain code parity symbols, with a focus on unique encoding methods and blockchain-based consensus mechanisms that aim to exceed 100,000 TPS (transactions per second) by leveraging distributed messaging queue technology.

## Key Features

- **Proof of Replication and Geolocation:** Our system incorporates proof of replication inspired by Filecoin and proof of geolocation based on cutting-edge research ([read more](https://eprint.iacr.org/2021/697.pdf)).
  
- **Utility Tokens:** We introduce two utility tokens for bandwidth and storage. Contributors receive tokens for every byte provided to the network, facilitating a fair and efficient resource exchange model.

- **Scalability Protocol:** Leveraging  ZeroMQ's scalability protocol, we ensure robust communication and scalability for the network.

- **Permissioned Blockchain:** Initially designed as permissioned for security, our blockchain architecture allows for seamless evolution to accommodate various use cases and consensus mechanisms.

## Project Foundation

The project draws inspiration from ZeroMQ's libraries, and has a dependency on the [Malamute](https://github.com/zeromq/malamute) C project and aims to build a barebones infrastructure capable of supporting decentralized CDNs while remaining adaptable to specific use cases.

## Getting Started

To get started with our project, please refer to the [documentation](https://bhare1985.github.io/mosaic) for installation instructions, development guidelines, and more.

We welcome contributions and feedback from the community to help shape the future of decentralized data distribution.

## Security Considerations:

While the data storage nodes operate in a permissionless manner, the blockchain initially employs a permissioned model. This approach prioritizes security during development and will be transitioned to a permissionless model once robust mechanisms to mitigate malicious actors are implemented.


## Features

- [Modern CMake practices](https://pabloariasal.github.io/2018/02/19/its-time-to-do-cmake-right/)
- Suited for single header libraries and projects of any scale
- Clean separation of library and executable code
- Integrated test suite
- Continuous integration via [GitHub Actions](https://help.github.com/en/actions/)
- Code coverage via [codecov](https://codecov.io)
- Code formatting enforced by [clang-format](https://clang.llvm.org/docs/ClangFormat.html) and [cmake-format](https://github.com/cheshirekow/cmake_format) via [Format.cmake](https://github.com/TheLartians/Format.cmake)
- Reproducible dependency management via [CPM.cmake](https://github.com/TheLartians/CPM.cmake)
- Installable target with automatic versioning information and header generation via [PackageProject.cmake](https://github.com/TheLartians/PackageProject.cmake)
- Automatic [documentation](https://bhare1985.github.io/mosaic) and deployment with [Doxygen](https://www.doxygen.nl) and [GitHub Pages](https://pages.github.com)

## Usage

### Build and run the standalone target

Use the following command to build and run the executable target.

```bash
cmake -S standalone -B build/standalone
cmake --build build/standalone
./build/standalone/Mosaic --help
```

### Build and run test suite

Use the following commands from the project's root directory to run the test suite.

```bash
cmake -S test -B build/test
cmake --build build/test
CTEST_OUTPUT_ON_FAILURE=1 cmake --build build/test --target test

# or simply call the executable: 
./build/test/MosaicTests
```

To collect code coverage information, run CMake with the `-DENABLE_TEST_COVERAGE=1` option.


### Build the documentation

The documentation is automatically built and [published](https://bhare1985.github.io/mosaic) whenever a [GitHub Release](https://help.github.com/en/github/administering-a-repository/managing-releases-in-a-repository) is created.
To manually build documentation, call the following command.

```bash
cmake -S documentation -B build/doc
cmake --build build/doc --target GenerateDocs
# view the docs
open build/doc/doxygen/html/index.html
```

To build the documentation locally, you will need Doxygen, jinja2 and Pygments installed on your system.

### Build everything at once

The project also includes an `all` directory that allows building all targets at the same time.
This is useful during development, as it exposes all subprojects to your IDE and avoids redundant builds of the library.

```bash
cmake -S all -B build
cmake --build build

# run tests
./build/test/MosaicTests
# format code
cmake --build build --target fix-format
# run standalone
./build/standalone/Mosaic --help
# build docs
cmake --build build --target GenerateDocs
```

### Additional tools

The test and standalone subprojects include the [tools.cmake](cmake/tools.cmake) file which is used to import additional tools on-demand through CMake configuration arguments.
The following are currently supported.

#### Sanitizers

Sanitizers can be enabled by configuring CMake with `-DUSE_SANITIZER=<Address | Memory | MemoryWithOrigins | Undefined | Thread | Leak | 'Address;Undefined'>`.

#### Static Analyzers

Static Analyzers can be enabled by setting `-DUSE_STATIC_ANALYZER=<clang-tidy | iwyu | cppcheck>`, or a combination of those in quotation marks, separated by semicolons.
By default, analyzers will automatically find configuration files such as `.clang-format`.
Additional arguments can be passed to the analyzers by setting the `CLANG_TIDY_ARGS`, `IWYU_ARGS` or `CPPCHECK_ARGS` variables.

#### Ccache

Ccache can be enabled by configuring with `-DUSE_CCACHE=<ON | OFF>`.

## FAQ

> Is this ready for production?

No
