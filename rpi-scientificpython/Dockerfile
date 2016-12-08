FROM resin/rpi-raspbian
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential pkg-config \
        python3-dev python3-pip \
        gfortran libblas-dev liblapack-dev \
        libjpeg-dev libjpeg62-turbo-dev liblcms2-dev liblzma-dev libtiff5-dev libwebp-dev \
        libfreetype6-dev libpng12-dev \
        libsuitesparse-dev \
 && rm -rf /var/lib/apt/lists/*
RUN pip3 install -v --upgrade pip wheel setuptools
RUN pip3 install -v --upgrade --no-cache-dir cython && \
    pip3 install -v --upgrade --no-cache-dir numpy  && \
    pip3 install -v --upgrade --no-cache-dir pillow && \
    pip3 install -v --upgrade --no-cache-dir matplotlib && \
    pip3 install -v --upgrade --no-cache-dir scipy && \
    pip3 install -v --upgrade --no-cache-dir scikit-learn

