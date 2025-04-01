FROM rocker/rstudio:4.2.2

ENV USER="rstudio" PASSWORD="&{ rspassw }" ROOT="TRUE"

ARG bioc_ver=3.16

RUN apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
        libhdf5-dev \
        libcurl4-gnutls-dev \
        libssl-dev \
        libxml2-dev \
        libpng-dev \
        libxt-dev \
        zlib1g-dev \
        libbz2-dev \
        liblzma-dev \
        libglpk40 \
        libgit2-dev \
    && apt-get clean all && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN Rscript -e "install.packages(c('rmarkdown', 'tidyverse', 'workflowr', 'BiocManager'));"
RUN Rscript -e "BiocManager::install(version = '${bioc_ver}')"

WORKDIR /home/rstudio
RUN ln -s /opt/spcs/stage /home/rstudio/stage