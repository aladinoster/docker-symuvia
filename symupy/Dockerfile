FROM continuumio/miniconda3

# Set the ENTRYPOINT to use bash
# (this is also where you’d set SHELL,
# if your version of docker supports this)
# ENTRYPOINT ["/bin/bash", "-c"]

# Open ports
EXPOSE 5000

# Libraries + Compiler
# RUN apt-get update && apt-get install -y
# wget bzip2 ca-certificates \
# xz-utils \
# build-essential \ 
# curl \   
# git

# Entry point
ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]

# Install packages interface
RUN ["/bin/bash","-c","conda install -c conda-forge -c licit-lab python=3.8 jupyterlab symupy"]