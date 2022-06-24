FROM jupyter/datascience-notebook

USER $NB_UID

RUN mamba install --quiet --yes \
    'spacy' \
    'gh' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"
    
RUN python -m spacy download en_core_web_sm && \
    python -m spacy download en_core_web_trf

RUN pip install --no-cache-dir torch torchvision torchaudio

RUN pip install jupyterlab-git

RUN jupyter labextension install jupyterlab-plotly

RUN fix-permissions /home/$NB_USER
