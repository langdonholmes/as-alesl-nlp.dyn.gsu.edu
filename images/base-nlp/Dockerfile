FROM jupyter/pyspark-notebook

USER root

RUN echo "envs_dirs:" >> "${CONDA_DIR}/.condarc" && \
    echo "  - /home/jovyan/conda_envs/" >> "${CONDA_DIR}/.condarc" && \
    fix-permissions "${CONDA_DIR}"
    
USER $NB_UID
    
RUN mamba install --quiet --yes \
    'spacy' \
    'nltk' \
    'gensim' \
    'gh' \
    'nb_conda_kernels' && \
    mamba clean --all -f -y
    
RUN pip install --no-cache-dir torch && \
    pip install jupyterlab-git && \
    jupyter labextension install jupyterlab-plotly
    
RUN python -m spacy download en_core_web_sm && \
    python -m spacy download en_core_web_trf && \
    python -m nltk.downloader all
