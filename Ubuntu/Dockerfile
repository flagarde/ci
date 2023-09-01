FROM ubuntu:20.04 AS base
ENV DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash","-o","pipefail","-c"]
ARG compiler
RUN case $compiler in \
    "clang-5")\
      apt-get update ;\
      apt-get install --no-install-recommends -y gcc-10-base=10.3.0-1ubuntu1~20.04 ;\
      apt-mark hold gcc-10-base ;;\
    esac &&\
    apt-mark hold libsystemd0 &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ xenial main" | tee -a "/etc/apt/sources.list.d/xenial.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ xenial universe" | tee -a "/etc/apt/sources.list.d/xenial.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ xenial-updates main" | tee -a "/etc/apt/sources.list.d/xenial-updates.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ xenial-updates universe" | tee -a "/etc/apt/sources.list.d/xenial-updates.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty main" | tee -a "/etc/apt/sources.list.d/trusty.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty universe" | tee -a "/etc/apt/sources.list.d/trusty.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty-updates main" | tee -a "/etc/apt/sources.list.d/trusty-updates.list" >/dev/null &&\
    echo "deb http://archive.ubuntu.com/ubuntu/ trusty-updates universe" | tee -a "/etc/apt/sources.list.d/trusty-updates.list" >/dev/null &&\
    apt-get update &&\
    apt-get install --no-install-recommends -y wget gpg ca-certificates &&\
    wget -q -O - "https://keyserver.ubuntu.com/pks/lookup?search=0xE1DD270288B4E6030699E45FA1715D88E1DF1F24&fingerprint=on&op=get" | gpg -q --dearmor - | tee "/usr/share/keyrings/git.gpg" > /dev/null &&\
    wget -q -O - "https://apt.llvm.org/llvm-snapshot.gpg.key" | gpg -q --dearmor - | tee "/usr/share/keyrings/llvm.gpg" >/dev/null &&\
    case $compiler in \
    "clang-3.9")\
      echo "deb [signed-by=/usr/share/keyrings/git.gpg] https://ppa.launchpadcontent.net/git-core/ppa/ubuntu xenial main" | tee -a "/etc/apt/sources.list.d/git.list" >/dev/null ;\
      echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/xenial/ llvm-toolchain-xenial-3.9 main" | tee -a "/etc/apt/sources.list.d/llvm-3.9.list" >/dev/null ;;\
    "clang-4")\
      echo "deb [signed-by=/usr/share/keyrings/git.gpg] https://ppa.launchpadcontent.net/git-core/ppa/ubuntu xenial main" | tee -a "/etc/apt/sources.list.d/git.list" >/dev/null ;\
      echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/xenial/ llvm-toolchain-xenial-4.0 main" | tee -a "/etc/apt/sources.list.d/llvm-4.list" >/dev/null ;;\
    *)\
      echo "deb [signed-by=/usr/share/keyrings/git.gpg] https://ppa.launchpadcontent.net/git-core/ppa/ubuntu jammy main" | tee -a "/etc/apt/sources.list.d/git.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ jammy main" | tee -a "/etc/apt/sources.list.d/jammy.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ jammy universe" | tee -a "/etc/apt/sources.list.d/jammy.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ jammy-updates main" | tee -a "/etc/apt/sources.list.d/jammy-updates.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ jammy-updates universe" | tee -a "/etc/apt/sources.list.d/jammy-updates.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ bionic main" | tee -a "/etc/apt/sources.list.d/bionic.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ bionic universe" | tee -a "/etc/apt/sources.list.d/bionic.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ bionic-updates main" | tee -a "/etc/apt/sources.list.d/bionic-updates.list" >/dev/null ;\
      echo "deb http://archive.ubuntu.com/ubuntu/ bionic-updates universe" | tee -a "/etc/apt/sources.list.d/bionic-updates.list" >/dev/null ;;\
    esac &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/bionic/ llvm-toolchain-bionic-7 main" | tee -a "/etc/apt/sources.list.d/llvm-7.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/bionic/ llvm-toolchain-bionic-8 main" | tee -a "/etc/apt/sources.list.d/llvm-8.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-9 main" | tee -a "/etc/apt/sources.list.d/llvm-9.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-10 main" | tee -a "/etc/apt/sources.list.d/llvm-10.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-11 main" | tee -a "/etc/apt/sources.list.d/llvm-11.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-12 main" | tee -a "/etc/apt/sources.list.d/llvm-12.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-13 main" | tee -a "/etc/apt/sources.list.d/llvm-13.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-14 main" | tee -a "/etc/apt/sources.list.d/llvm-14.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal-15 main" | tee -a "/etc/apt/sources.list.d/llvm-15.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/llvm.gpg] http://apt.llvm.org/focal/ llvm-toolchain-focal main" | tee -a "/etc/apt/sources.list.d/llvm.list" >/dev/null &&\
    wget -q -O - "https://apt.kitware.com/keys/kitware-archive-latest.asc" | gpg -q --dearmor - | tee "/usr/share/keyrings/kitware.gpg" >/dev/null &&\
    echo 'deb [signed-by=/usr/share/keyrings/kitware.gpg] https://apt.kitware.com/ubuntu/ focal main' | tee "/etc/apt/sources.list.d/kitware.list" >/dev/null &&\
    echo 'deb [signed-by=/usr/share/keyrings/kitware.gpg] https://apt.kitware.com/ubuntu/ focal-rc main' | tee -a "/etc/apt/sources.list.d/kitware-rc.list" >/dev/null && \
    wget -q -O - "https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB" | gpg -q --dearmor - | tee "/usr/share/keyrings/oneapi.gpg" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/oneapi.gpg] https://apt.repos.intel.com/oneapi all main" | tee "/etc/apt/sources.list.d/oneAPI.list" >/dev/null &&\
    wget -q -O - "https://keyserver.ubuntu.com/pks/lookup?search=0x1E9377A2BA9EF27F&fingerprint=on&op=get" | gpg -q --dearmor - | tee "/usr/share/keyrings/toolchains.gpg" > /dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/toolchains.gpg] http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu xenial main" | tee -a "/etc/apt/sources.list.d/toolchains-xenial.list" >/dev/null &&\
    echo "deb [signed-by=/usr/share/keyrings/toolchains.gpg] http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu precise main" | tee -a "/etc/apt/sources.list.d/toolchains-precise.list" >/dev/null &&\
    apt-get update &&\
    apt-get install --no-install-recommends -y binutils make &&\
    apt-get remove -y wget gpg &&\
    apt-get dist-upgrade --no-install-recommends -y; apt-get autoremove -y; apt-get clean -y

FROM base AS compiler
ARG compiler
ARG tests
WORKDIR .
COPY tests ./tests/
ENV DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash","-o","pipefail","-c"]
RUN case $compiler in \
    "gcc-4.4")\
      apt-get install --no-install-recommends -y g++-4.4;\
      export CC=gcc-4.4; export CXX=g++-4.4; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.4.7; export CXX_COMPILER_VERSION=4.4.7 ;;\
    "gcc-4.5")\
      apt-get install --no-install-recommends -y g++-4.5;\
      export CC=gcc-4.5; export CXX=g++-4.5; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.5.3; export CXX_COMPILER_VERSION=4.5.3 ;;\
    "gcc-4.6")\
      apt-get install --no-install-recommends -y g++-4.6;\
      export CC=gcc-4.6; export CXX=g++-4.6; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.6.4; export CXX_COMPILER_VERSION=4.6.4 ;;\
    "gcc-4.7")\
      apt-get install --no-install-recommends -y g++-4.7;\
      export CC=gcc-4.7; export CXX=g++-4.7; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.7.4; export CXX_COMPILER_VERSION=4.7.4 ;;\
    "gcc-4.8")\
      apt-get install --no-install-recommends -y g++-4.8;\
      export CC=gcc-4.8; export CXX=g++-4.8; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.8.5; export CXX_COMPILER_VERSION=4.8.5 ;;\
    "gcc-4.9")\
      apt-get install --no-install-recommends -y g++-4.9;\
      export CC=gcc-4.9; export CXX=g++-4.9; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.9.4; export CXX_COMPILER_VERSION=4.9.4 ;;\
    "gcc-5")\
      apt-get install --no-install-recommends -y g++-5;\
      export CC=gcc-5; export CXX=g++-5; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=5.5.0; export CXX_COMPILER_VERSION=5.5.0 ;;\
    "gcc-6")\
      apt-get install --no-install-recommends -y g++-6;\
      export CC=gcc-6; export CXX=g++-6; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=6.5.0; export CXX_COMPILER_VERSION=6.5.0 ;;\
    "gcc-7")\
      apt-get install --no-install-recommends -y g++-7;\
      export CC=gcc-7; export CXX=g++-7; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=7.5.0; export CXX_COMPILER_VERSION=7.5.0 ;;\
    "gcc-8")\
      apt-get install --no-install-recommends -y g++-8;\
      export CC=gcc-8; export CXX=g++-8; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=8.4.0; export CXX_COMPILER_VERSION=8.4.0 ;;\
    "gcc-9")\
      apt-get install --no-install-recommends -y g++-9;\
      export CC=gcc-9; export CXX=g++-9; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=9.5.0; export CXX_COMPILER_VERSION=9.5.0 ;;\
    "gcc-10")\
      apt-get install --no-install-recommends -y g++-10;\
      export CC=gcc-10; export CXX=g++-10; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=10.4.0; export CXX_COMPILER_VERSION=10.4.0 ;;\
    "gcc-11")\
      apt-get install --no-install-recommends -y g++-11;\
      export CC=gcc-11; export CXX=g++-11; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=11.3.0; export CXX_COMPILER_VERSION=11.3.0 ;;\
    "gcc-12")\
      apt-get install --no-install-recommends -y g++-12;\
      export CC=gcc-12; export CXX=g++-12; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=12.1.0; export CXX_COMPILER_VERSION=12.1.0 ;;\
    "clang-3.5")\
      apt-get install --no-install-recommends -y clang-3.5;\
      export CC=clang-3.5; export CXX=clang++-3.5; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.5.2; export CXX_COMPILER_VERSION=3.5.2 ;;\
    "clang-3.6")\
      apt-get install --no-install-recommends -y clang-3.6;\
      export CC=clang-3.6; export CXX=clang++-3.6; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.6.2; export CXX_COMPILER_VERSION=3.6.2 ;;\
    "clang-3.7")\
      apt-get install --no-install-recommends -y clang-3.7;\
      export CC=clang-3.7; export CXX=clang++-3.7; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.7.1; export CXX_COMPILER_VERSION=3.7.1 ;;\
    "clang-3.8")\
      apt-get install --no-install-recommends -y clang-3.8;\
      export CC=clang-3.8; export CXX=clang++-3.8; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.8.0; export CXX_COMPILER_VERSION=3.8.0 ;;\
    "clang-3.9")\
      apt-get install --no-install-recommends -y clang-3.9;\
      export CC=clang-3.9; export CXX=clang++-3.9; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.9.1; export CXX_COMPILER_VERSION=3.9.1 ;;\
    "clang-4")\
      apt-get install --no-install-recommends -y clang-4.0;\
      export CC=clang-4.0; export CXX=clang++-4.0; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=4.0.0; export CXX_COMPILER_VERSION=4.0.0 ;;\
    "clang-5")\
      apt-get install --no-install-recommends -y clang-5.0;\
      export CC=clang-5.0; export CXX=clang++-5.0; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=5.0.1; export CXX_COMPILER_VERSION=5.0.1 ;;\
    "clang-6")\
      apt-get install --no-install-recommends -y clang-6.0;\
      export CC=clang-6.0; export CXX=clang++-6.0; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=6.0.1; export CXX_COMPILER_VERSION=6.0.1 ;;\
    "clang-7")\
      apt-get install --no-install-recommends -y clang-7 libc++1-7;\
      export CC=clang-7; export CXX=clang++-7; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=7.0.1; export CXX_COMPILER_VERSION=7.0.1 ;;\
    "clang-8")\
      apt-get install --no-install-recommends -y clang-8 libc++1-8;\
      export CC=clang-8; export CXX=clang++-8; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=8.0.1; export CXX_COMPILER_VERSION=8.0.1 ;;\
    "clang-9")\
      apt-get install --no-install-recommends -y clang-9 libc++1-9;\
      export CC=clang-9; export CXX=clang++-9; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=9.0.1; export CXX_COMPILER_VERSION=9.0.1 ;;\
    "clang-10")\
      apt-get install --no-install-recommends -y clang-10 libc++1-10;\
      export CC=clang-10; export CXX=clang++-10; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=10.0.1; export CXX_COMPILER_VERSION=10.0.1 ;;\
    "clang-11")\
      apt-get install --no-install-recommends -y clang-11 libc++1-11;\
      export CC=clang-11; export CXX=clang++-11; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=11.1.0; export CXX_COMPILER_VERSION=11.1.0 ;;\
    "clang-12")\
      apt-get install --no-install-recommends -y clang-12 libc++1-12;\
      export CC=clang-12; export CXX=clang++-12; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=12.0.1; export CXX_COMPILER_VERSION=12.0.1 ;;\
    "clang-13")\
      apt-get install --no-install-recommends -y clang-13 libc++1-13;\
      export CC=clang-13; export CXX=clang++-13; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=13.0.1; export CXX_COMPILER_VERSION=13.0.1 ;;\
    "clang-14")\
      apt-get install --no-install-recommends -y clang-14 libc++1-14;\
      export CC=clang-14; export CXX=clang++-14; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=14.0.6; export CXX_COMPILER_VERSION=14.0.6 ;;\
    "clang-15")\
      apt-get install --no-install-recommends -y clang-15 libc++1-15;\
      export CC=clang-15; export CXX=clang++-15; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=15.0.6; export CXX_COMPILER_VERSION=15.0.6 ;;\
    *)\
      echo "No compiler provided !";\
      echo "GCC Available : gcc-4.4, gcc-4.5, gcc-4.6, gcc-4.7, gcc-4.8, gcc-4.9, gcc-5, gcc-6, gcc-7, gcc-8, gcc-9, gcc-10, gcc-11, gcc-12";\
      echo "Clang Available : clang-3.5, clang-3.6, clang-3.7, clang-3.8, clang-3.9, clang-4, clang-5, clang-6, clang-7, clang-8, clang-9, clang-10, clang-11, clang-12, clang-13, clang-14, clang-15";;\
    esac &&\
    case $C_COMPILER_ID in \
    "GNU")\
      ln -s /usr/bin/$CC /usr/bin/gcc ;\
      ln -s /usr/bin/$CXX /usr/bin/g++ ;;\
    "Clang")\
      ln -s /usr/bin/$CC /usr/bin/clang ;\
      ln -s /usr/bin/$CXX /usr/bin/clang++ ;;\
    esac &&\
    apt-get upgrade; apt-get autoremove -y ; apt-get clean -y &&\
    echo "** make --version :" &&\
    make --version &&\
    echo "** CC --version :" &&\
    $CC --version &&\
    echo "** CXX --version :" &&\
    $CXX --version &&\
    echo "** C_COMPILER_ID=$C_COMPILER_ID, C_COMPILER_VERSION=$C_COMPILER_VERSION" &&\
    echo "** CXX_COMPILER_ID=$CXX_COMPILER_ID, CXX_COMPILER_VERSION=$CXX_COMPILER_VERSION" &&\
    case $tests in \
    "true")\
      apt-get install --no-install-recommends -y cmake ;\
      cmake -B ./build -S ./tests ;\
      if [ $? -eq 0 ];\
        then exit 0;\
        else exit 1;\
      fi;\
      cmake --build ./build ;\
      if [ $? -eq 0 ];\
        then exit 0;\
        else exit 1;\
      fi;\
      rm -rf ./build ;\
    esac &&\
    rm -rf ./tests \
