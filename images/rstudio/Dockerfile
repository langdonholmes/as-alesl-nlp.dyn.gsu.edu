FROM jupyter/r-notebook

RUN python3 -m pip install jupyter-rsession-proxy

#RUN cd /tmp/ && \
#    git clone --depth 1 https://github.com/jupyterhub/jupyter-server-proxy && \
#    cd jupyter-server-proxy/jupyterlab-server-proxy && \
#    npm install && npm run build && jupyter labextension link . && \
#    npm run build && jupyter lab build

USER root

# Needed by RStudio
RUN apt-get update -qq --yes && \
    apt-get install --yes --no-install-recommends -qq \
        psmisc \
        sudo \
        libapparmor1 \
        lsb-release \
        cmake \
        libpq5 \
        libclang-dev > /dev/null

# apt packages needed for R packages
#RUN apt update --yes > /dev/null && \
#    apt install --no-install-recommends --yes \

ENV RSTUDIO_URL https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2022.02.3-492-amd64.deb
RUN curl --silent --location --fail ${RSTUDIO_URL} > /tmp/rstudio.deb && \
    dpkg -i /tmp/rstudio.deb && \
    rm /tmp/rstudio.deb

#ENV SHINY_SERVER_URL https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.17.973-amd64.deb
#RUN curl --silent --location --fail ${SHINY_SERVER_URL} > /tmp/shiny-server.deb && \
#    dpkg -i /tmp/shiny-server.deb && \
#    rm /tmp/shiny-server.deb

RUN mamba install --quiet --yes \
    'r-hmisc' \
    'r-lme4' \
    'r-lmertest' \
    'r-psych' \
    'r-nlme' \
    'r-randomforest' \
    'r-car' \
    'r-rstatix' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"
    
ENV PATH=$PATH:/usr/lib/rstudio-server/bin
USER $NB_USER
