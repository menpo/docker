FROM menpo/rpi-menpoproject-lean
RUN apt-get update && apt-get install -y --no-install-recommends \
        cmake \
        libboost-python-dev \
 && rm -rf /var/lib/apt/lists/*
RUN curl https://codeload.github.com/davisking/dlib/tar.gz/v19.2 | tar xz && \
    cd ./dlib-*/tools/python                                              && \
    mkdir build                                                           && \
    cd build                                                              && \
    cmake                                                                    \
        -DPYTHON3=ON                                                         \
         ..                                                               && \
    cmake --build . --config Release                                      && \
    mv dlib.so /usr/local/lib/python3.*/dist-packages/                    && \
    cd ../../../../ && rm -rf ./dlib-*

