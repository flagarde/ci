FROM archlinux:base AS base
SHELL ["/bin/bash","-o","pipefail","-c"]
RUN pacman-key --init &&\
    pacman-key --populate archlinux &&\
    pacman --noconfirm --noprogressbar -Syu &&\
    pacman --sync --needed --noconfirm --noprogressbar wget sudo fakeroot binutils make gcc patch &&\
    useradd user --shell /bin/bash --create-home --home-dir /var/user &&\
    passwd --lock user &&\
    mkdir -p /etc/sudoers.d &&\
    echo "user ALL=(ALL) NOPASSWD: /usr/bin/pacman" > "/etc/sudoers.d/allow_user_to_pacman" &&\
    echo "user ALL=(ALL) NOPASSWD: /usr/bin/trizen" > "/etc/sudoers.d/allow_user_to_trizen" &&\
    echo "root ALL=(ALL) CWD=* ALL" > "/etc/sudoers.d/permissive_root_Chdir_Spec" &&\
    mkdir -p /var/user/trizen &&\
    chmod a+rxw -R /var/user/ &&\
    wget -q -P /var/user/trizen https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=trizen &&\
    mv /var/user/trizen/PKGBUILD?h=trizen /var/user/trizen/PKGBUILD &&\
    sudo -S -u user -D /var/user/trizen bash -c "makepkg -s --noprogressbar --noconfirm --needed" &&\
    pacman --upgrade --needed --noconfirm --noprogressbar /var/user/trizen/trizen-1:1.66-1-any.pkg.tar.zst &&\
    rm -rf /var/user/trizen/

FROM base AS compiler
ARG compiler
ARG tests
SHELL ["/bin/bash","-o","pipefail","-c"]
RUN case $compiler in \
    "gcc-4.3")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc43 ;\
      export CC=gcc-4.3; export CXX=g++-4.3; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.3.6; export CXX_COMPILER_VERSION=4.3.6 ;;\
    "gcc-4.4")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc44 ;\
      export CC=gcc-4.4; export CXX=g++-4.4; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.4.7; export CXX_COMPILER_VERSION=4.4.7 ;;\
    "gcc-4.5")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc45 ;\
      export CC=gcc-4.5; export CXX=g++-4.5; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.5.4; export CXX_COMPILER_VERSION=4.5.4 ;;\
    "gcc-4.6")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc46 ;\
      export CC=gcc-4.6; export CXX=g++-4.6; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.6.4; export CXX_COMPILER_VERSION=4.6.4 ;;\
    "gcc-4.7")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc47 ;\
      export CC=gcc-4.7; export CXX=g++-4.7; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.7.4; export CXX_COMPILER_VERSION=4.7.4 ;;\
    "gcc-4.8")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc48 ;\
      export CC=gcc-4.8; export CXX=g++-4.8; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.8.5; export CXX_COMPILER_VERSION=4.8.5 ;;\
    "gcc-4.9")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc49 ;\
      export CC=gcc-4.9; export CXX=g++-4.9; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=4.9.4; export CXX_COMPILER_VERSION=4.9.4 ;;\
    "gcc-5")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc5 ;\
      export CC=gcc-5; export CXX=g++-5; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=5.5.0; export CXX_COMPILER_VERSION=5.5.0 ;;\
    "gcc-6")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc6 ;\
      export CC=gcc-6; export CXX=g++-6; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=6.5.0; export CXX_COMPILER_VERSION=6.5.0 ;;\
    "gcc-7")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc7 ;\
      export CC=gcc-7; export CXX=g++-7; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=7.5.0; export CXX_COMPILER_VERSION=7.5.0 ;;\
    "gcc-8")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc8 ;\
      export CC=gcc-8; export CXX=g++-8; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=8.4.0; export CXX_COMPILER_VERSION=8.4.0 ;;\
    "gcc-9")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc9 ;\
      export CC=gcc-9; export CXX=g++-9; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=9.4.0; export CXX_COMPILER_VERSION=9.4.0 ;;\
    "gcc-10")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc10 ;\
      export CC=gcc-10; export CXX=g++-10; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=10.4.0; export CXX_COMPILER_VERSION=10.4.0 ;;\
    "gcc-11")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc11 ;\
      export CC=gcc-11; export CXX=g++-11; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=11.3.0; export CXX_COMPILER_VERSION=11.3.0 ;;\
    "gcc-12")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar gcc ;\
      export CC=gcc-12; export CXX=g++-12; export C_COMPILER_ID=GNU; export CXX_COMPILER_ID=GNU; export C_COMPILER_VERSION=12.1.1; export CXX_COMPILER_VERSION=12.1.1 ;;\
    "clang-3.5")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang35 ;\
      export CC=clang-3.5; export CXX=clang++-3.5; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=3.5.2; export CXX_COMPILER_VERSION=3.5.2 ;;\
    "clang-4")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang40 ;\
      export CC=clang-4.0; export CXX=clang++-4.0; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=4.0.1; export CXX_COMPILER_VERSION=4.0.1 ;;\
    "clang-5")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang50 ;\
      export CC=clang-5.0; export CXX=clang++-5.0; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=5.0.2; export CXX_COMPILER_VERSION=5.0.2 ;;\
    "clang-7")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang70 ;\
      export CC=clang-7; export CXX=clang++-7; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=7.0.1; export CXX_COMPILER_VERSION=7.0.1 ;;\
    "clang-8")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang8 ;\
      export CC=clang-8; export CXX=clang++-8; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=8.0.1; export CXX_COMPILER_VERSION=8.0.1 ;;\
    "clang-9")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang9 ;\
      export CC=clang-9; export CXX=clang++-9; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=9.0.1; export CXX_COMPILER_VERSION=9.0.1 ;;\
    "clang-10")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang10 ;\
      export CC=clang-10; export CXX=clang++-10; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=10.0.1; export CXX_COMPILER_VERSION=10.0.1 ;;\
    "clang-13")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang13 ;\
      export CC=clang-13; export CXX=clang++-13; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=13.0.1; export CXX_COMPILER_VERSION=13.0.1 ;;\
    "clang-14")\
      sudo -S -u user trizen -S --needed --noconfirm --noprogressbar clang ;\
      export CC=clang-14; export CXX=clang++-14; export C_COMPILER_ID=Clang; export CXX_COMPILER_ID=Clang; export C_COMPILER_VERSION=14.0.6; export CXX_COMPILER_VERSION=14.0.6 ;;\
    *)\
      echo "No compliler provided !";\
      echo "GCC Available : gcc-4.3, gcc-4.4, gcc-4.5, gcc-4.6, gcc-4.7, gcc-4.8, gcc-4.9, gcc-5, gcc-6, gcc-7, gcc-8, gcc-9, gcc-10, gcc-11, gcc-12";\
      echo "Clang Available : clang-3.5, clang-4, clang-5, clang-7, clang-8, clang-9, clang-10, clang-13, clang-14";;\
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
      pacman  install --no-install-recommends -y cmake ;\
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
    pacman -Rscn gcc &&\
    rm -rf ./tests
