FROM menpo/rpi-menpoproject-lean

# dlib install
# Note that this only just compiles on a RPI3 with nothing else much running
# (needs approx. 1GB of RAM to compile some components)
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

# OpenCV 3 install, adapted from
# http://www.pyimagesearch.com/2016/04/18/install-guide-raspberry-pi-3-raspbian-jessie-opencv-3/
RUN apt-get update && apt-get install -y --no-install-recommends                     \
        build-essential                                                              \
        cmake                                                                        \
        pkg-config                                                                   \
        libjpeg-dev                                                                  \
        libtiff5-dev                                                                 \
        libjasper-dev                                                                \
        libpng12-dev                                                                 \
        libavcodec-dev                                                               \
        libavformat-dev                                                              \
        libswscale-dev                                                               \
        libv4l-dev                                                                   \
        libxvidcore-dev                                                              \
        libx264-dev                                                                  \
        libatlas-base-dev                                                            \
        gfortran                                                                     \
 && rm -rf /var/lib/apt/lists/*
RUN curl https://codeload.github.com/opencv/opencv/tar.gz/3.1.0         | tar xz  && \
    curl https://codeload.github.com/opencv/opencv_contrib/tar.gz/3.1.0 | tar xz  && \
    cd opencv-*                                                                   && \
    mkdir build                                                                   && \
    cd build                                                                      && \
    cmake                                                                            \
        -D CMAKE_BUILD_TYPE=RELEASE                                                  \
        -D CMAKE_INSTALL_PREFIX=/usr/local                                           \
        -D INSTALL_PYTHON_EXAMPLES=ON                                                \
        -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.1.0/modules              \
        -D BUILD_EXAMPLES=ON                                                         \
        ..                                                                        && \
    make -j4                                                                      && \
    make install && ldconfig                                                      && \
    rm -rf ../../opencv*

# cyvlfeat/vlfeat install
# We have to use a specially modified version of vlfeat that we can
# compile for linux armv7. See the forked repo cloned below for details.
# Also note that we run the full menpo test suite again (it should all work,
# including cyvlfeat deps)
RUN curl https://codeload.github.com/jabooth/vlfeat/tar.gz/rpi | tar xz      && \
    curl https://codeload.github.com/menpo/cyvlfeat/tar.gz/v0.4.5 | tar xz   && \
    cd vlfeat-*                                                              && \
    make -j4                                                                 && \
    cp bin/*/libvl.so /usr/local/lib/                                        && \
    mkdir /usr/local/include/vl                                              && \
    cp vl/*.h /usr/local/include/vl/                                         && \
    ldconfig                                                                 && \
    cd ..                                                                    && \
    pip3 install -v --no-cache-dir ./cyvlfeat-*                              && \
    rm -rf ./*vlfeat*                                                        && \
    nosetests menpo

# FFMPEG Install
# We trust the prebuild binary from here for now :)
# https://github.com/ccrisan/motioneye/wiki/Install-On-Raspbian
RUN curl https://raw.githubusercontent.com/wiki/ccrisan/motioneye/precompiled/ffmpeg_3.1.1-1_armhf.deb > ffmpeg.deb && \
    dpkg -i ffmpeg*.deb                                                                                             && \
    rm ffmpeg*.deb

