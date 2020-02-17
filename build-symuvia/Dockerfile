FROM ubuntu:18.04
LABEL maintainer="Andres Ladino <aladinoster@gmail.com>"

USER root

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update && apt-get install -y \
    wget bzip2 ca-certificates \
    xz-utils \
    build-essential \ 
    curl \   
    git \
    xqilla \
    libboost-all-dev \
    aptitude \
    gdal-bin \
    rapidjson-dev \
    libgdal-dev \
    unixodbc &&\
    aptitude search -y \
    boost \
    && rm -rf /var/lib/apt/lists/* \
    && curl -SL http://releases.llvm.org/9.0.0/clang+llvm-9.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz \
    | tar -xJC . && \
    mv clang+llvm-9.0.0-x86_64-linux-gnu-ubuntu-18.04 clang_9.0.0 && \
    echo 'export PATH=/clang_9.0.0/bin:$PATH' >> ~/.bashrc && \
    echo 'export LD_LIBRARY_PATH=/clang_9.0.0/lib:$LD_LIBRARY_PATH' >> ~/.bashrc

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini

RUN chmod +x /usr/bin/tini

RUN git clone https://github.com/aladinoster/build-symuvia.git --depth=1 \
    --branch master --single-branch home/build-symuvia

ADD SymuVia.tar.gz /home/build-symuvia/SymuVia/src/

ADD SymuCore.tar.gz /home/build-symuvia/SymuCore/src/

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]