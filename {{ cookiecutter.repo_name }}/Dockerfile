FROM continuumio/miniconda3

ADD environment.yml /tmp/environment.yml
RUN conda env create -f /tmp/environment.yml

RUN echo "source activate {{ cookiecutter.repo_name }}" > ~/.bashrc
ENV PATH /opt/conda/envs/{{ cookiecutter.repo_name }}/bin:$PATH

ARG USER=tester
ARG UID=1000
ARG GID=1000
RUN addgroup --gid ${GID} ${USER} \
 && adduser \
    --disabled-password \
    --gecos ${USER} \
    --gid ${GID} \
    --uid ${UID} \
    ${USER}

ARG APP_DIR=/home/${USER}/app
RUN mkdir -p ${APP_DIR} \
 && chown ${UID}:${GID} ${APP_DIR}

WORKDIR ${APP_DIR}

USER ${USER}

COPY --chown=${USER}:${USER} . .
RUN pip install -e .

ENV SHELL /bin/bash