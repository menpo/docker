FROM menpo/rpi-scientificpython
WORKDIR /menpo
# Get hold of curl to download and mock/nose for menpo testing
RUN apt-get update && apt-get install -y --no-install-recommends \
        curl \
 && rm -rf /var/lib/apt/lists/* && \
    pip3 install --no-cache-dir mock nose
# Install latest menpo project releases from github
# And test that all menpo's unit tests pass
RUN curl https://codeload.github.com/menpo/menpo/tar.gz/v0.7.4        | tar xz && pip3 install --no-cache-dir ./menpo-*        && rm -r ./menpo-*        && \
    curl https://codeload.github.com/menpo/menpowidgets/tar.gz/v0.2.1 | tar xz && pip3 install --no-cache-dir ./menpowidgets-* && rm -r ./menpowidgets-* && \
    curl https://codeload.github.com/menpo/menpofit/tar.gz/v0.4.1     | tar xz && pip3 install --no-cache-dir ./menpofit-*     && rm -r ./menpofit-*     && \
    curl https://codeload.github.com/menpo/menpodetect/tar.gz/v0.4.1  | tar xz && pip3 install --no-cache-dir ./menpodetect-*  && rm -r ./menpodetect-*  && \
    nosetests -a '!cyvlfeat' menpo
## Setup for notebook access
EXPOSE 8888
RUN mkdir -p -m 700 /root/.jupyter/ && \
    echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py
CMD ["jupyter", "notebook", "--no-browser"]

