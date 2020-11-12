FROM peridigm/netcdf

LABEL maintainer="John Foster <johntfosterjr@gmail.com>"

ENV HOME /root

RUN apt-get -yq install g++ \ 
                        gfortran \
                        python \ 
                        libblas-dev \
                        liblapack-dev \
                        libboost-dev \
                        cmake  \
                        git \
                        libyaml-cpp-dev

#Build Trilinos
RUN git clone https://github.com/trilinos/Trilinos.git trilinos; \
    git checkout trilinos-release-13-0-0; \
    mkdir trilinos/build
ADD trilinos-debian-cmake.sh /trilinos/build/trilinos-debian-cmake.sh
RUN cd trilinos/build; \
    ./trilinos-debian-cmake.sh; \
    make && make install; \
    cd ../..; \
    rm -rf trilinos

