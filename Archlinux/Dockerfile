FROM archlinux:base AS base
SHELL ["/bin/bash","-o","pipefail","-c"]
WORKDIR .
RUN pacman-key --init 2>/dev/null &&\
    pacman-key --populate archlinux 2>/dev/null &&\
    pacman -Sy &&\
    pacman -Syu --noconfirm --noprogressbar &&\
    pacman -S --noconfirm --noprogressbar --needed sudo wget fakeroot binutils patch make diffutils &&\
    useradd --create-home container &&\
    passwd --lock container &&\
    echo "container ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers &&\
    sudo usermod -aG wheel container &&\
    sudo chown -R container /home/container &&\
    export BUILDDIR=/home/container/makepkg/builddir &&\
    export PKGDEST=/home/container/makepkg/pkgdest &&\
    export SRCDEST=/home/container/makepkg/srcdest &&\
    su -c "wget -P /home/container/trizen https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=trizen" container &&\
    su -c "mv /home/container/trizen/PKGBUILD?h=trizen /home/container/trizen/PKGBUILD" container &&\
    cd /home/container/trizen/ &&\
    su -c "makepkg -s -i --noconfirm" container &&\
    rm -rf /home/container/makepkg/ ; rm -rf /home/container/trizen/

FROM base AS compiler-base
SHELL ["/bin/bash","-o","pipefail","-c"]
RUN pacman --noconfirm --noprogressbar -S gcc

FROM compiler-base AS compiler
SHELL ["/bin/bash","-o","pipefail","-c"]
WORKDIR .
COPY compilers ./compilers/
WORKDIR .
COPY tests ./tests/
ARG compiler
RUN sudo chown -R container ./compilers/ &&\
    case $compiler in \
    "gcc-4.3"|"gcc-4.4"|"gcc-4.5"|"gcc-4.6"|"gcc-4.7"|"gcc-4.8")\
      cd ./compilers/osl ;\
      su -c "makepkg -s -i --noconfirm" container ;\
      cd ../../compilers/cloog ;\
      su -c "makepkg -s -i --noconfirm" container ;\
      pacman -Rscn --noconfirm --noprogressbar texlive-bin texlive-core ;;\
    esac &&\
    case $compiler in \
    "gcc-4.3")\
      cd ../../compilers/gcc43 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.3/gcc; export CXX=/opt/gcc-4.3/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.3.6; export CXX_COMPILER_VERSION=4.3.6 ;;\
    "gcc-4.4")\
      cd ../../compilers/gcc44 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.4/gcc; export CXX=/opt/gcc-4.4/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.4.7; export CXX_COMPILER_VERSION=4.4.7 ;;\
    "gcc-4.5")\
      cd ../../compilers/gcc45 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.5/gcc; export CXX=/opt/gcc-4.5/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.5.4; export CXX_COMPILER_VERSION=4.5.4 ;;\
    "gcc-4.6")\
      cd ../../compilers/gcc46 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.6/gcc; export CXX=/opt/gcc-4.6/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.6.4; export CXX_COMPILER_VERSION=4.6.4 ;;\
    "gcc-4.7")\
      cd ../../compilers/gcc47 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.7/gcc; export CXX=/opt/gcc-4.7/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.7.4; export CXX_COMPILER_VERSION=4.7.4 ;;\
    "gcc-4.8")\
      cd ../../compilers/gcc48 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.8/gcc; export CXX=/opt/gcc-4.8/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.8.5; export CXX_COMPILER_VERSION=4.8.5 ;;\
    "gcc-4.9")\
      cd ../../compilers/gcc49 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-4.9/gcc; export CXX=/opt/gcc-4.9/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.9.4; export CXX_COMPILER_VERSION=4.9.4 ;;\
    "gcc-5")\
      cd ../../compilers/gcc5 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-5/gcc; export CXX=/opt/gcc-5/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=5.5.0; export CXX_COMPILER_VERSION=5.5.0 ;;\
    "gcc-6")\
      cd ../../compilers/gcc6 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-6/gcc; export CXX=/opt/gcc-6/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=6.5.0; export CXX_COMPILER_VERSION=6.5.0 ;;\
    "gcc-7")\
      cd ../../compilers/gcc7 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-7/gcc; export CXX=/opt/gcc-7/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=7.5.0; export CXX_COMPILER_VERSION=7.5.0 ;;\
    "gcc-8")\
      cd ../../compilers/gcc8 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-8/gcc; export CXX=/opt/gcc-8/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=8.5.0; export CXX_COMPILER_VERSION=8.5.0 ;;\
    "gcc-9")\
      cd ../../compilers/gcc9 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-9/gcc; export CXX=/opt/gcc-9/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=9.5.0; export CXX_COMPILER_VERSION=9.5.0 ;;\
    "gcc-10")\
      cd ../../compilers/gcc10 &&\
      su -c "makepkg -s -i --noconfirm" container ;\
      export CC=/opt/gcc-10/gcc; export CXX=/opt/gcc-10/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=10.4.0; export CXX_COMPILER_VERSION=10.4.0 ;;\
    "gcc-11")\
      pacman -S --noconfirm --noprogressbar gcc11 ;\
      export CC=/opt/gcc-11/gcc; export CXX=/opt/gcc-11/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=11.3.0; export CXX_COMPILER_VERSION=11.3.0 ;;\
    "gcc-12")\
      pacman -S --noconfirm --noprogressbar gcc ;\
      export CC=/opt/gcc-12/gcc; export CXX=/opt/gcc-12/g++; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=12.1.1; export CXX_COMPILER_VERSION=12.1.1 ;;\
    "clang-3.5")\
      trizen -S --noconfirm --noprogressbar clang35 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.5.2; export CXX_COMPILER_VERSION=3.5.2 ;;\
    "clang-4")\
      trizen -S --noconfirm --noprogressbar clang40 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=4.0.1; export CXX_COMPILER_VERSION=4.0.1 ;;\
    "clang-5")\
      trizen -S --noconfirm --noprogressbar clang50 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=5.0.2; export CXX_COMPILER_VERSION=5.0.2 ;;\
    "clang-6")\
      trizen -S --noconfirm --noprogressbar clang60 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=4.3.6; export CXX_COMPILER_VERSION=4.3.6 ;;\
    "clang-7")\
      trizen -S --noconfirm --noprogressbar clang70 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=7.0.1; export CXX_COMPILER_VERSION=7.0.1 ;;\
    "clang-8")\
      trizen -S --noconfirm --noprogressbar clang8 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=8.0.1; export CXX_COMPILER_VERSION=8.0.1 ;;\
    "clang-9")\
      trizen -S --noconfirm --noprogressbar clang9 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=9.0.1; export CXX_COMPILER_VERSION=9.0.1 ;;\
    "clang-10")\
      trizen -S --noconfirm --noprogressbar clang10 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=10.0.1; export CXX_COMPILER_VERSION=10.0.1 ;;\
    "clang-11")\
      trizen -S --noconfirm --noprogressbar clang11 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=4.3.6; export CXX_COMPILER_VERSION=4.3.6 ;;\
    "clang-12")\
      trizen -S --noconfirm --noprogressbar clang12 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=4.3.6; export CXX_COMPILER_VERSION=4.3.6 ;;\
    "clang-13")\
      trizen -S --noconfirm --noprogressbar clang13 ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=13.0.1; export CXX_COMPILER_VERSION=13.0.1 ;;\
    "clang-14")\
      trizen -S --noconfirm --noprogressbar clang ;\
      export CC=clang; export CXX=clang++; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=14.0.6; export CXX_COMPILER_VERSION=14.0.6 ;;\
    esac &&\
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
      pacman -S --noconfirm --noprogressbar cmake ;\
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
