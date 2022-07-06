FROM jupyter/pyspark-notebook

USER ${NB_UID}

RUN conda install \
    -c pytorch \
    --repodata-fn repodata.json \
    --quiet --yes \
    pytorch \
    cudatoolkit=11.6

RUN echo "envs_dirs:" >> "${CONDA_DIR}/.condarc" && \
    echo "  - /home/jovyan/conda_envs/" >> "${CONDA_DIR}/.condarc" && \
    fix-permissions "${CONDA_DIR}"

RUN mamba install --quiet --yes \
        'nltk' \
        'gensim' \
        'gh' \
        'nb_conda_kernels' \
        'spacy' \
    && mamba clean --all -f -y \
    && pip install \
        jupyterlab-git \
        transformers \
        spacy-transformers \
    && jupyter labextension install jupyterlab-plotly \
    && fix-permissions "${CONDA_DIR}" \
    && fix-permissions "/home/${NB_USER}"

RUN python -m spacy download en_core_web_trf
