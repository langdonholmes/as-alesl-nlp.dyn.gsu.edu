FROM jupyter/pyspark-notebook

USER ${NB_UID}

RUN echo "envs_dirs:" >> "${CONDA_DIR}/.condarc" && \
    echo "  - /home/jovyan/conda_envs/" >> "${CONDA_DIR}/.condarc" && \
    fix-permissions "${CONDA_DIR}"
        
RUN conda update --all --yes \
    && conda install -c pytorch -c conda-forge --quiet --yes \
        pytorch \
        torchvision \
        torchaudio \
        cudatoolkit=11.6 \
RUN conda install -c huggingface --quiet --yes \
        transformers \
    && mamba install --quiet --yes \
        'nltk' \
        'gensim' \
        'gh' \
        'nb_conda_kernels' \
        'spacy' \
        'spacy-transformers' \
    && mamba clean --all -f -y \
    && pip install \
        jupyterlab-git \
        transformers \
    && jupyter labextension install jupyterlab-plotly \
    && fix-permissions "${CONDA_DIR}" \
    && fix-permissions "/home/${NB_USER}"

RUN python -m spacy download en_core_web_trf
