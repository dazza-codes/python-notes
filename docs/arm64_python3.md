# ARM64 - Apple Silicon M1

## Glossary

- Intel architectures: x86_64, amd64, linux/amd64
- ARM architectures: AArch64, arm64, linux/arm64

## Apple Silicon (M1) Systems

M1 is not just a processor core, it is an integrated System on Chip (SoM)

- all components are integrated
- the purchase options can’t be upgraded later
- there are no separate graphics GPUs
- there are no upgrade options for RAM
- All performance tests indicate that Apple M1-pro and M1-max SoC can out
  perform x86_64 systems, so the benefits of Apple Silicon are substantial
  - the catches are:
    - M1 is an ARM system that has software compatibility issues
    - M1 is a proprietary ARM architecture, it might not be available on cloud
      systems (at a reasonable price/performance point)
      - AWS have their own ARM architectures (Graviton, Graviton2)
      - https://youtu.be/ObfxS7x0UdY
      - RaspberryPi is an ARM architecture
- Open Source Software compatibility
  - Homebrew 3.x started to support Apple Silicon
    - [3.0.0 — Homebrew](https://brew.sh/2021/02/05/homebrew-3.0.0/)
    - Not all packages are built for arm64 platforms, some packages need Rosetta
      emulations for amd64 binaries
  - [GitHub - conda-forge/miniforge: A conda-forge distribution.](https://github.com/conda-forge/miniforge)
    - supports various CPU architectures (x86_64, ppc64le, and aarch64 including
      Apple M1)
    - Apple silicon builds are experimental and haven’t had testing like the
      other platforms (as of Dec, 2021)
    - defaults to conda-forge packages
    - Supports
      [GitHub - mamba-org/mamba: The Fast Cross-Platform Package Manager](https://github.com/mamba-org/mamba)
      - https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-MacOSX-arm64.sh
- If using Apple Silicon is reasonable, choices are necessary for several user
  groups
  - choices between M1, M1-pro, and M1-max configurations
    - 14” models vs. 16” models
  - M1-pro allows 16Gb or 32Gb RAM
  - M1-max starts at 32Gb RAM, allows up to 64Gb RAM
  - https://youtu.be/yYCIXiYg3Nc (15 min architecture guide)
  - https://youtu.be/W1Ks_NcnM7k (15 min buyers guide)
    - M1-pro 14” base model is the new default (forget original M1)
      - \$20 upgrade for the power supply
      - Supports up to 2 external monitors
      - General users might upgrade to 1Tb SSD, but skip all other upgrades
      - Power users who need a small 14” form factor might also opt to upgrade
        for 10 CPU cores and 32Gb RAM, but should be encouraged to go with a 16”
        model (at a similar price point)
    - M1-max 16” model for power users
      - https://link.medium.com/U2OmUcNvjmb
        - Commentary about data science on Apple Silicon and where it could
          benefit python PyData stacks and Machine Learning (ML)
        - Benefits from more CPU/GPU cores
        - Some benefits depend on library support for native arm64 build
          (Rosetta translations are slower)
        - “setting up Python with data science and non-data science packages on
          the new Mac models was a nightmare” and using native builds from
          Anaconda/miniconda are recommended
      - https://youtu.be/PfeFuAFoCs0
        - performance comparison on base model vs. upgrades
        - 1 Tb SSD is worth it for larger SSD and faster write speeds with
          faster SSD caching if RAM runs low
        - M1-max starts at 32 Gb RAM with 2x faster memory bandwidth; similar
          CPU performance with M1-pro and M1-max when both have 10 CPU cores
      - power users will benefit from multi-core workloads with more data-heavy
        applications (e.g. scientists, developers, data scientists); since the
        RAM is fixed on the system on chip (SoC) design, the longevity of the
        laptop is better with 32 Gb RAM
      - The number of GPU cores required depends on the applications; for most
        users, 16 GPU cores are sufficient
      - Recommend: 10 core CPU, >= 32 Gb RAM, >= 1Tb SSD
        - supports 4 external monitors on M1-max 16” model
        - Better cooling (required for more GPUs); although this can add noise
          and reduce battery life
        - Better GPU computing, but only if algorithms and libraries are built
          to take advance of it (e.g. not CUDA)
  - What is the support to multiple external monitors?
    - M1-pro is required to support up to 2x external monitors
    - M1-max is required to support up to 4x external monitors

## YouTube Background on M1 Architectures

Apple M1 is an ARM System on Chip (SoC) Architecture (more on this below)

- https://youtu.be/vqs_0W-MSB0
- https://youtu.be/vg0AF166eVI

## IDEs on M1

- Does it support arm64 natively?
- Does it support remote development on cloud systems for arm64 or amd64?
- Can it support cross-compilations?

### VSCode

### PyCharm (Pro)

## Python on M1 arm64 vs. Intel amd64

- Alex Ziskind on python for M1
  - https://youtu.be/2Acht_5_HTo
  - https://youtu.be/H06R4tXXWZ0
  - OSX on M1 ships with python 2.7 (deprecated, but required by OSX)
  - Homebrew can install python3 (3.9)
    - Some tools provide initial support for M1, with caveats, such as the Pants
      build tools, see
      [Prerequisites](https://www.pantsbuild.org/docs/prerequisites#macos)
  - Conda installations can provide python built for arm64 (3.9)
- Anaconda / miniconda for python 3.x and environments
  - https://www.anaconda.com/blog/apple-silicon-transition
  - https://coiled.io/blog/apple-arm64-mambaforge/
    - August 2021
    - recommends using Mambaforge-MacOSX-arm64 installer
  - Use miniforge ?
    - https://youtu.be/\_CO-ND1FTOU
  - Intel/amd64 packages requires Rosetta for amd64 emulations (could be slow?)
    - some bugs in Rosetta are a black box that OSS cannot fix
  - conda native support for arm64 on M1?
    - What is mambaforge ?
    - miniforge with arm64 libs
      - defaults to python 3.9.x
      - Can provide other python versions
      - Can it provide python 3.7? Are we forced to upgrade to 3.8 or 3.9?
    - Running PyData libraries on an Apple M1 machine requires you to use an
      ARM64-tailored version of conda-forge
  - Some PyTorch algorithms use NVidea CUDA libs that will never run on Apple
    Silicon systems
    - Problems for Machine Learning?
    - ML on the Apple neural engine?
  - Even if working on arm64 (M1) laptops is feasible for daily development
    work, is it compatible for cloud deployments?
    - AWS has Graviton2 arm64 systems
  - Do python packages work as expected?
    - Depends whether the packages are built for arm64 and any M1 specific
      architecture details
    - Some packages might need extra work to install from source on arm64 -
      build tool chains and system dependencies can be buggy
  - Even if python and packages work on arm64 for M1, is it compatible for cloud
    deployments?
    - https://aws.amazon.com/ec2/graviton/ is an arm64 platform with silicon
      designed by AWS; this option begs many questions, such as:
      - is it compatible with Apple Silicon arm64?
      - can our gitlab-CI services use K8s with graviton arm instances?
      - Should docker builds use base images that provide tool chains to build
        for arm64 (Ubuntu and amazon Linux and red hat support it)
    - What are the consequences of dev/test builds on arm64-M1 and then
      deploying to arm64-Graviton or amd64-Intel systems? How are bugs resolved
      by developers? If developers create make recipes and other practices that
      are tailored for arm64-M1, how can they efficiently switch a dev/test
      workflow to work on a remote system running amd64-Intel?
    - Even if cloud deployments can use Apple Silicon instances, is it cost
      effective vs. Intel instances?
  - How to ensure that packages and docker builds are not generating bloated
    universal builds?
  - What happens to cross-compilations when building on M1 for docker that will
    be deployed on amd64?
  -

> When you install a library written for Intel CPU architecture, the code will
> be run through the Rosetta emulator. This often works great but may cause
> unexpected problems for specific PyData libraries. For example, I personally
> encountered this with Dask’s memory usage blowing up when importing a \<100MB
> dataset. Since the internals of Rosetta is proprietary, there’s no way to know
> exactly why this is happening.

- Python versions compiled for arm64
  - miniconda?
  - conda-forge packages ?
- Scientific/GIS python relies on c/c++ libs including
  - Numpy
  - Rasterio / GDAL
    - https://launchpad.net/ubuntu/focal/arm64/gdal-bin
  - Shapely / GEOS
  - Proj
  - ML libs - PyTorch
  - GPU acceleration - NVidia CUDA - gone!
- Notebooks and clusters
  - Jupyter notebooks
  - Dask and Tornado cluster computing
  - PySpark (and Spark on arm64 vs. amd64)
- Rosetta emulations for amd64 instruction sets
  - Translates intel-code onto arm64 M1

## Warranties

- Could using open-source tools on Apple hardware invalidate warranties?

## Source Code Compilers for c/c++ and Fortran

The Apple M1 is not a standard arm64 platform. Since M1 has Apple proprietary
technology, it could take a long time to reverse engineer details of the system
and for compilers and drivers to catch up. Some proprietary compilers might get
support from Apple; open source compilers will not get Apple support. According
to the Asahi-Linux project, the Apple boot loader allows for alternative
operating systems and the process of reverse engineering drivers might not
infringe Apple IP.

- QEMU emulation and cross-compilations
- Universal binaries (support for both amd64 and arm64)
- Conda on arm64 might provide the tool chain required?
  - e.g. `conda install cmake llvm-openmp compilers`

## ARM Architectures

- https://youtu.be/7LqPJGnBPMM
  - ARM: Advanced RISC Machines
    - Spun off from Acorn Computers, with investment from Apple et al
    - Focused on Intellectual Property for ARM architectures
  - RISC: Reduced Instruction Set Computing
  - ARM Ltd licenses the architecture IP to partners (a large community of
    companies in the semi-conductor industry)
  - ARM architecture versions and extensions
    - ARMv7, ARMv8, ARMv9
  - Embedded Cortex-M\* processors (low power, restricted capabilities)
  - Embedded Cortex-R\* processors (higher power, wider capabilities) for
    real-time controllers
  - Cortex-A\* processors for application platform operating systems, with
    memory management systems and support for multi-core systems
  - arm64 - is this defined by Linux as the ARMv8 platform?
- https://youtu.be/GyWyikB2hFs - ARM vs RISC-V
- https://youtu.be/NNol7fRGo2E
  - ARM is an architecture specification with many versions and many
    implementations of each version
  - Any specific architecture version, such as ARMv8, should be capable of
    executing the same code (with some caveats for 32 vs. 64 bit instruction
    sets and SOC components)
    - ARMv8-A supports **AArch64** for 64 bit instruction sets, with are
      optional, it also supports an **AArch32** mode for 32 bit compatibility
      with ARMv7-A
    - ARMv8 cores: Cortex-A32 (32 bit), Cortex-A53, Cortex-A57, etc
  - Many different implementations for each ARM specification, with different
    power and performance profiles
  - Many different ways to build System on Chip (SOC) with ARM to design
    specific solutions for various use cases and each of these designs can have
    many different implementations:
    - ARMv7-A for Applications that support operating systems with RAM, cache,
      IO etc
    - ARMv7-M for Microcontrollers that have lower power consumption and
      specific use-cases
    - ARMv7-R for Real time systems with deterministic performance
- AWS Graviton Systems
  - https://youtu.be/kAg7U2I2hzQ
    - Graviton2
      - AWS custom System on Chip (SoC) with ARM64 Neoverse N1 core
      - ARM v8.2 compliant
      - _Every vCPU is a physical core_ (no hyper threading, SMT)
    - `lscpu` reports the `Architecture:  aarch64`
    - T4g, M6g, R6g, C6g instance types
      - the additional `d` suffix has local NVMe SSD local storage
    - up to 40% better price-performance vs. x86_64 instances
    - Programming languages are widely supported
      - compiled languages need to target the arm64 platform
      - https://github.com/aws/aws-graviton-getting-started
  - https://youtu.be/ObfxS7x0UdY
    - Docker builds for AArch64 on GitHub actions
  - Docker cross compilation and multi-platform builds
    - https://www.docker.com/blog/getting-started-with-docker-for-arm-on-linux/
    - https://www.docker.com/blog/faster-multi-platform-builds-dockerfile-cross-compilation-guide/
    - QEMU to emulate arm64 when building on an amd64 system
    - https://docs.docker.com/buildx/working-with-buildx/
    - `docker buildx build —platform linux/amd64 .` (x86_64)
    - `docker buildx build —platform linux/arm64 .` (AArch64)
    - It might be more efficient to use separate builds for each platform with
      tags to identify the images (rather than universal builds that use runtime
      behavior to choose the platform)

## Internet Evaluations and Opinions

- Python on M1 ARM is not ready for Enterprise Development
  - https://link.medium.com/DChM0wUjmlb

> I made the decision three months ago to buy three new team members at Deep
> Discovery new M1 Macbooks and I am here to tell you as a technical leader: the
> M1 is not ready for software development teams using compiled languages or
> tools or any stack that depends on them. The support in the open source
> ecosystem is still very poor. You should wait until M1 processors are more
> widely deployed, open source support accumulates and then make the jump.

- Don’t program on an M1 Mac
  - Alex Ziskind is one of _the_ authorities on working with Apple Silicon; his
    YouTube channel is packed with reasonable, balanced evaluations of
    everything on M1
  - https://youtu.be/Mp1q1SFGOKI
    - Max out the RAM option because it’s fixed at purchase because M1 is a SoC
      platform (no upgrades); developers need a lot of RAM, to run a development
      IDE app, simulators, emulators, database services and docker images for
      micro-services running in a local K8s dev-system, along many browser tabs
      open
    - Support for external devices, e.g. multiple monitors, may take a while
    - Wait for release of more powerful laptops and desktops, to allow the
      product line to mature and software support to catch up

## Virtual Machines on M1

- UTM is a native OS-X / iOS app for running virtual machines
  - https://mac.getutm.app/
  - It puts a GUI on QEMU for emulating CPU architectures

## Native Linux on M1

- https://youtu.be/rZozRzw36wU
  - M1 is _not_ a standards-compliant arm64 system, it is Apple IP that requires
    Apple collaboration to work on, which is not likely to be provided to the
    open-source Linux community

### Asahi Linux

- https://asahilinux.org/about/

> Asahi Linux is a project and community with the goal of porting Linux to Apple
> Silicon Macs, starting with the 2020 M1 Mac Mini, MacBook Air, and MacBook
> Pro.\
> Our goal is not just to make Linux run on these machines but to polish
> it to the point where it can be used as a daily OS. Doing this requires a
> tremendous amount of work, as Apple Silicon is an entirely undocumented
> platform. In particular, we will be reverse engineering the Apple GPU
> architecture and developing an open-source driver for it.

## Docker on ARM64 (Apple Silicon)

- https://youtu.be/He8JMyHRbBw
  - rosetta can be required for builds that need x86 libs

When a docker build uses a linux container on a Mac-M1-OSX system, the
underlying build tool-chain relies on emulation or cross-compilation for the x86
or amd64 instruction set. Doing some google searches for relevant keywords like
`docker x86 amd64 apple silicon M1` etc. turns up useful items, e.g.

- https://medium.com/swlh/building-x86-64-docker-containers-on-apple-silicon-a6d868a18f37

Interesting note (worth noting that things move along quickly on the bleeding
edge, so it might be a bit out dated by now):

> qemu does not work perfectly, and most of its use in Docker seems to be from
> people on x86_64 architectures building for arm, so any bugs the other way are
> likely to just be popping up now that M1s are being distributed.

- the macbook M1 can build images for amd64/x86_64 with an option:
  - `docker buildx build --platform linux/amd64 -t ${IMAGE}`
- the macbook M1 will have problems building images for its native arch arm64
  where linux libs/pkgs have no arm64 builds in repos

## Remote Development (Using cloud amd64)

- https://www.jetbrains.com/help/pycharm/configuring-product-to-work-on-the-vm.html
- https://www.jetbrains.com/help/pycharm/big-data-tools-configuration.html
- https://www.jetbrains.com/help/pycharm/remote-development-starting-page.html
- https://www.jetbrains.com/help/pycharm/remote-development-starting-page.html
- https://www.jetbrains.com/help/pycharm/remote-development-overview.html
- this looks interesting, it has a "Gateway" app for Apple Silicon that connects
  to a remote PyCharm IDE
- e.g. run Ubuntu on remote docker-machine and use snap to install PyCharm (pro)
  on it, then use "Gateway" to connect via docker-machine ssh credentials

## CI/CD Systems

- Can CI/CD systems build with arm64 systems? Should they?
- If CI/CD systems fail on amd64, how is that debugged by developers working on
  arm64 laptops?
- How many changes are required to project configs and make recipes to allow for
  simultaneous development / CI on arm64/amd64 systems?

## Cloud Deployments

- How prevalent is arm64 on cloud systems?
- What does it cost vs. amd64?
- How does it perform vs. amd64?
