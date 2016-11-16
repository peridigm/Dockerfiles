FROM peridigm/netcdf

MAINTAINER John T. Foster <johntfosterjr@gmail.com>

ENV HOME /root

RUN apt-get -yq install g++ \ 
                        gfortran \
                        python \ 
                        libblas-dev \
                        liblapack-dev \
                        libboost-dev \
                        cmake  \
                        git

#Build Trilinos
RUN git clone https://github.com/trilinos/Trilinos.git trilinos; \
    mkdir trilinos/build
ADD trilinos-debian-cmake.sh /trilinos/build/trilinos-debian-cmake.sh
RUN cd trilinos/build; \
    ./trilinos-debian-cmake.sh; \
    make -j8 && make install; \
    cd ../..; \
    rm -rf trilinos

