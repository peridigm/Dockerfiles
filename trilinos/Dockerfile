FROM peridigm/netcdf

LABEL maintainer="John Foster <johntfosterjr@gmail.com>"

ENV HOME /root

RUN apt-get -yq install g++ \ 
                        gfortran \
                        python3 \
                        libblas-dev \
                        liblapack-dev \
                        libboost-dev \
                        cmake  \
                        git \
                        libyaml-cpp-dev

#Build Trilinos
RUN git clone https://github.com/trilinos/Trilinos.git trilinos; \
    git checkout trilinos-release-13-2-0; \
    mkdir trilinos/build
ADD trilinos-debian-cmake.sh /trilinos/build/trilinos-debian-cmake.sh
RUN cd trilinos/build; \
    ./trilinos-debian-cmake.sh; \
    make -j8 && make install; \
    cd ../..; \
    rm -rf trilinos

