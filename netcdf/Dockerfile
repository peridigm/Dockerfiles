FROM debian:bookworm

LABEL maintainer="John Foster <johntfosterjr@gmail.com>"

ENV HOME /root

RUN apt-get update
RUN apt-get -yq install gcc \
                        build-essential \
                        wget \
                        bzip2 \
                        tar \
                        zlib1g-dev \
                        m4 \
                        libopenmpi-dev \
                        openmpi-bin \
                        openssh-server \
                        file \
                        libcurl4-openssl-dev

#Build HDF5
RUN wget https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.12/hdf5-1.12.0/src/hdf5-1.12.0.tar.bz2; \
    tar xjvf hdf5-1.12.0.tar.bz2; \
    cd hdf5-1.12.0; \
    ./configure --enable-parallel --enable-shared --with-default-api-version=v110 --prefix=/usr/local/hdf5; \
    make; \
    make install; \
    cd ..; \
    rm -rf hdf5-1.12.0 hdf5-1.12.0.tar.bz2 

#Build netcdf
RUN wget https://github.com/Unidata/netcdf-c/archive/v4.7.4.tar.gz; \
    tar xzvf v4.7.4.tar.gz
ADD largefiles.patch netcdf-c-4.7.4/largefiles.patch
RUN cd netcdf-c-4.7.4; \
    patch -p1 < largefiles.patch; \
    ./configure --prefix=/usr/local/netcdf \ 
                CC=mpicc \
                LDFLAGS=-L/usr/local/hdf5/lib \
                CFLAGS=-I/usr/local/hdf5/include; \
    make; \
    make install;\
    cd ..;\
    rm -rf netcdf-c-4.7.4 v4.7.4.tar.gz
