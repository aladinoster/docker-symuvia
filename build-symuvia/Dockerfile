FROM continuumio/miniconda3

# Set the ENTRYPOINT to use bash
# (this is also where you’d set SHELL,
# if your version of docker supports this)
# ENTRYPOINT ["/bin/bash", "-c"]

# Open ports
EXPOSE 5000

# Libraries + Compiler
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
    unixodbc \
    libpq-dev &&\
    aptitude search -y \
    boost \
    && rm -rf /var/lib/apt/lists/* \
    && curl -SL http://releases.llvm.org/9.0.0/clang+llvm-9.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz \
    | tar -xJC . && \
    mv clang+llvm-9.0.0-x86_64-linux-gnu-ubuntu-18.04 clang_9.0.0 && \
    echo 'export PATH=/clang_9.0.0/bin:$PATH' >> ~/.bashrc && \
    echo 'export LD_LIBRARY_PATH=/clang_9.0.0/lib:$LD_LIBRARY_PATH' >> ~/.bashrc

# Build Cmake
RUN git clone https://github.com/aladinoster/build-symuvia.git --depth=1 \
    --branch master --single-branch home/build-symuvia

# Source Files
COPY SymuVia/ /home/build-symuvia/SymuVia/src/

COPY SymuCore/ /home/build-symuvia/SymuCore/src/

# Manual version of Xqilla
RUN curl -SL https://sourceforge.net/projects/xqilla/files/XQilla-2.3.4.tar.gz/download -o XQilla-2.3.4.tar.gz  &&\
    tar -xzvf XQilla-2.3.4.tar.gz -C /home/ &&\
    mv /home/XQilla-2.3.4/include/ /usr/local/

# Setting home directory
WORKDIR /home/build-symuvia

# Entry point
ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]

# Conda install
RUN ["/bin/bash","-c","conda install -y -c conda-forge cmake"]

# Compile Symuvia
RUN mkdir -p build && cd build && \
    cmake .. && \ 
    cmake --build .