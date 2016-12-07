FROM resin/rpi-raspbian
WORKDIR /menpo
RUN echo 'deb-src http://archive.raspbian.org/raspbian jessie main contrib non-free rpi firmware' >> /etc/apt/sources.list && \
    apt-get update --fix-missing && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential curl python3-dev python3-pip && \
    apt-get build-dep -y python-numpy python-scipy python-matplotlib cython pillow
RUN pip3 install --upgrade pip wheel setuptools && \
    pip3 install --upgrade cython               && \
    pip3 install --upgrade numpy                && \
    pip3 install --upgrade scipy pillow matplotlib scikit-learn mock nose
# Install latest menpo project releases from github 
RUN curl https://codeload.github.com/menpo/menpo/tar.gz/v0.7.4        | tar xz && pip3 install --no-cache-dir ./menpo-*        && rm -r ./menpo-*        && \
    curl https://codeload.github.com/menpo/menpowidgets/tar.gz/v0.2.1 | tar xz && pip3 install --no-cache-dir ./menpowidgets-* && rm -r ./menpowidgets-* && \
    curl https://codeload.github.com/menpo/menpofit/tar.gz/v0.4.1     | tar xz && pip3 install --no-cache-dir ./menpofit-*     && rm -r ./menpofit-*     && \
    curl https://codeload.github.com/menpo/menpodetect/tar.gz/v0.4.1  | tar xz && pip3 install --no-cache-dir ./menpodetect-*  && rm -r ./menpodetect-*  && \
    nosetests -a '!cyvlfeat' menpo
# Setup for notebook access
EXPOSE 8888
RUN mkdir -p -m 700 /root/.jupyter/ && \
    echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py
CMD ["jupyter", "notebook", "--no-browser"]

